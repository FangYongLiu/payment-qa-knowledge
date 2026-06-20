---
title: Botim-PayBy 报文加解密规范
domain: channel-integration
kind: wiki_page
slug: botim-payby-payload-security
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/1072791687
tags: []
---

# Botim-PayBy 报文加解密规范

本页定义 Botim ↔ PayBy 之间 gRPC 网关请求/响应 payload 的对称加密方案：使用 AES-256/GCM/NoPadding，IV(nonce) 拼接在密文之前并整体 Base64 编码。

## 加密参数

- 算法：`AES/GCM/NoPadding`
- 密钥长度：AES-256
- IV 长度：16 字符（Java 实现中 `GCM_NONCE_LENGTH = 12` 字节 nonce + `GCM_TAG_LENGTH = 16` 字节 tag）
- IV 处理：将随机生成的 nonce 拼接在密文前
- 编码：加密结果使用 Base64 编码后传输

适用对象：整个请求 payload（即 [[botim-payby-grpc-gateway-protocol]] 中 `ApplicationMessage` 的承载内容），密文形式在传输链路中保证安全。

## 加密流程

1. 生成随机 nonce（12 字节）
2. 用 `SecretKey` + `GCMParameterSpec(GCM_TAG_LENGTH * 8, nonce)` 初始化 `Cipher.ENCRYPT_MODE`
3. 对 plain bytes 执行 `cipher.doFinal`
4. 输出格式：`12 bytes nonce + encrypted bytes`
5. 整体 Base64 编码后再发送

### Java 加密示例

```java
public static byte[] encrypt(byte[] plain, SecretKey secretKey) throws Exception {
    // Generate Random Nonce
    byte[] nonce = new byte[GCM_NONCE_LENGTH];
    new SecureRandom().nextBytes(nonce);

    // Initialize GCM Cipher
    Cipher cipher = Cipher.getInstance(TRANSFORMATION);
    GCMParameterSpec spec = new GCMParameterSpec(GCM_TAG_LENGTH * 8, nonce);
    cipher.init(Cipher.ENCRYPT_MODE, secretKey, spec);

    // Execute
    byte[] ciphertext = cipher.doFinal(plain);

    // 12 bytes nonce + encrypted bytes
    ByteBuffer byteBuffer = ByteBuffer.allocate(nonce.length + ciphertext.length);
    byteBuffer.put(nonce);
    byteBuffer.put(ciphertext);
    return byteBuffer.array();
}
```

## 解密流程

1. 将 Base64 编码的 AES Key 转换为 `SecretKey`
2. 将 Base64 编码的密文解码为 byte 数组
3. 校验长度：必须 `>= GCM_NONCE_LENGTH + GCM_TAG_LENGTH`，否则视为非法（`Invalid encrypted data length`）
4. 从前 12 字节切出 nonce，剩余部分为密文
5. 使用相同的 `AES/GCM/NoPadding` + `GCMParameterSpec` 初始化 `Cipher.DECRYPT_MODE` 并执行 `doFinal`

### 关键常量

```java
private static final int GCM_TAG_LENGTH = 16;
private static final int GCM_NONCE_LENGTH = 12;
private static final String ALGORITHM = "AES";
private static final String TRANSFORMATION = "AES/GCM/NoPadding";
```

### Java 解密示例

```java
public static byte[] decrypt(byte[] encryptedData, SecretKey secretKey) throws Exception {
    // Parse nonce and encrypted bytes
    if (encryptedData.length < GCM_NONCE_LENGTH + GCM_TAG_LENGTH) {
        throw new IllegalArgumentException("Invalid encrypted data length");
    }
    ByteBuffer byteBuffer = ByteBuffer.wrap(encryptedData);
    byte[] nonce = new byte[GCM_NONCE_LENGTH];
    byteBuffer.get(nonce);
    byte[] ciphertext = new byte[encryptedData.length - GCM_NONCE_LENGTH];
    byteBuffer.get(ciphertext);

    // Initialize GCM Cipher
    Cipher cipher = Cipher.getInstance(TRANSFORMATION);
    GCMParameterSpec spec = new GCMParameterSpec(GCM_TAG_LENGTH * 8, nonce);
    cipher.init(Cipher.DECRYPT_MODE, secretKey, spec);

    // Execute
    return cipher.doFinal(ciphertext);
}

// 解密示例
public static String decryptText(String encryptedData, SecretKey secretKey) throws Exception {
    byte[] encrypted = Base64.getDecoder().decode(encryptedData);
    byte[] plain = decrypt(encrypted, secretKey);
    return new String(plain, StandardCharsets.UTF_8);
}
```

## 调用端使用示例

从 gRPC 响应 message 中取字节，使用 Base64 编码的 AES key 还原明文 JSON：

```java
String plainData = new String(
    AesGcmUtil.decryptText(
        new String(response.getMessage().toByteArray()),
        AesGcmUtil.fromBase64(TestConstant.AES_256_KEY_A)
    ).getBytes(),
    StandardCharsets.UTF_8);
```

## 数据格式约定

- 密文格式：`nonce(12B) || ciphertext(含 GCM tag)`
- 传输格式：上述字节数组的 Base64 字符串
- 明文格式：JSON 文本（UTF-8），即 `ApplicationMessage.amp` 的内容，例如：

```json
{
    "requestTime": 17691238142134,
    "bizContent": {
        "mobileNumber": "xxxx",
        "uid": "xxx"
    }
}
```

## 相关链接

- 网关协议与 `ApplicationMessage` 字段定义：[[botim-payby-grpc-gateway-protocol]]
- 整体集成方案与背景：[[botim-payby-server-integration-overview]]
- 加密 payload 承载的具体业务接口：[[api_personal_bind_customer]]、[[api_personal_login_or_refresh]]、[[api_personal_v3_auth_login]]

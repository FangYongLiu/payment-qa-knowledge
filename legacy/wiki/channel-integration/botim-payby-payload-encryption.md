---
title: Botim-PayBy报文加解密规范
domain: channel-integration
kind: wiki_page
slug: botim-payby-payload-encryption
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:a01637cc-4974-45c3-b1e9-d194dac7ed1f
tags: []
---

# Botim-PayBy报文加解密规范

本页描述 Botim 与 PayBy 之间 gRPC 网关请求中 `amp` 应用消息载荷（Application Message Payload）的 AES 加解密规则，以及 Java 加密与 Rust 二进制序列化的参考实现。上层协议结构与字段定义见 [[botim-payby-grpc-gateway-protocol]]。

## 算法与参数

请求载荷整体使用 AES 加密，密文形式在传输链路中传递。

- Key length：AES-256
- AES encryption algorithm：`AES/GCM/NoPadding`
- IV length：16 characters
- IV 值拼接在密文之前
- 加密结果使用 Base64 编码

实现常量（Java 参考值）：

| 常量 | 值 |
| --- | --- |
| `GCM_TAG_LENGTH` | 16 |
| `GCM_NONCE_LENGTH` | 12 |
| `ALGORITHM` | `AES` |
| `TRANSFORMATION` | `AES/GCM/NoPadding` |

## 加密流程（Payload Encryption）

加密结果格式：`12 bytes nonce + encrypted bytes`，最终再做 Base64 编码。

步骤：

1. 使用 `SecureRandom` 生成 `GCM_NONCE_LENGTH`（12 字节）随机 nonce
2. 用 `AES/GCM/NoPadding` 初始化 `Cipher`，`GCMParameterSpec` 的 tag 长度为 `GCM_TAG_LENGTH * 8` 位
3. `cipher.doFinal(plain)` 得到密文
4. 将 nonce 与密文按顺序写入 `ByteBuffer`，输出 `nonce || ciphertext`
5. 对最终字节数组进行 Base64 编码用于传输

### Java 加密示例

```java
public static byte[] encrypt(byte[] plain, SecretKey secretKey) throws Exception {
    byte[] nonce = new byte[GCM_NONCE_LENGTH];
    new SecureRandom().nextBytes(nonce);

    Cipher cipher = Cipher.getInstance(TRANSFORMATION);
    GCMParameterSpec spec = new GCMParameterSpec(GCM_TAG_LENGTH * 8, nonce);
    cipher.init(Cipher.ENCRYPT_MODE, secretKey, spec);

    byte[] ciphertext = cipher.doFinal(plain);

    ByteBuffer byteBuffer = ByteBuffer.allocate(nonce.length + ciphertext.length);
    byteBuffer.put(nonce);
    byteBuffer.put(ciphertext);
    return byteBuffer.array();
}
```

## 解密流程（Payload Decryption）

解密步骤：

1. 将 Base64 编码的 AES key 转换为 `SecretKey`
2. 将 Base64 编码的密文解码为 byte 数组
3. 使用 AES 解密：`algorithm: AES/GCM/NoPadding`，Key length: AES-256，IV length: 16 characters
4. 拆分 `12 bytes nonce + encrypted bytes`，使用 nonce 构造 `GCMParameterSpec` 后 `doFinal`

合法性校验：`encryptedData.length` 必须 `>= GCM_NONCE_LENGTH + GCM_TAG_LENGTH`，否则抛 `Invalid encrypted data length`。

### Java 解密示例

```java
public static byte[] decrypt(byte[] encryptedData, SecretKey secretKey) throws Exception {
    if (encryptedData.length < GCM_NONCE_LENGTH + GCM_TAG_LENGTH) {
        throw new IllegalArgumentException("Invalid encrypted data length");
    }
    ByteBuffer byteBuffer = ByteBuffer.wrap(encryptedData);
    byte[] nonce = new byte[GCM_NONCE_LENGTH];
    byteBuffer.get(nonce);
    byte[] ciphertext = new byte[encryptedData.length - GCM_NONCE_LENGTH];
    byteBuffer.get(ciphertext);

    Cipher cipher = Cipher.getInstance(TRANSFORMATION);
    GCMParameterSpec spec = new GCMParameterSpec(GCM_TAG_LENGTH * 8, nonce);
    cipher.init(Cipher.DECRYPT_MODE, secretKey, spec);
    return cipher.doFinal(ciphertext);
}

public static String decryptText(String encryptedData, SecretKey secretKey) throws Exception {
    byte[] encrypted = Base64.getDecoder().decode(encryptedData);
    byte[] plain = decrypt(encrypted, secretKey);
    return new String(plain, StandardCharsets.UTF_8);
}
```

调用示例：

```java
String plainData = new String(
    AesGcmUtil.decryptText(
        new String(response.getMessage().toByteArray()),
        AesGcmUtil.fromBase64(TestConstant.AES_256_KEY_A)
    ).getBytes(),
    StandardCharsets.UTF_8);
```

## Nonce 与密文格式约定

- 加密产物固定布局：前 12 字节为 nonce，紧跟密文（含 GCM tag）
- GCM tag 长度 16 字节包含在密文末尾，用于完整性校验
- 解密侧必须按相同布局先取 nonce 再取密文，长度不足直接判失败

## Application Message 二进制序列化（Rust 参考）

加解密的对象是经过二进制序列化的 Application Message。Rust 端通过 `ToBinRepr` / `FromBinRepr` trait 完成各字段的编码解码，编码规则如下：

| 字段 | 类型 | 二进制表示 |
| --- | --- | --- |
| `AMVer` | 版本 | 1 字节 |
| `AMID` | Request ID | 16 字节 UUID |
| `ASN` / `ASM` / `ADN` / `ADM` | 字符串 | u8 长度前缀 + UTF-8 字节 |
| `AMTrusty` | 字符串 | u16 长度前缀（big-endian） + UTF-8 字节 |
| `AMP` | 载荷字节 | u32 长度前缀（big-endian） + 字节内容 |
| `AMFlag` | 标志位 | 2 字节 |
| `AMHeaders` | Map | u8 数量 + N × (key:u8len+bytes, value:u16len+bytes) |
| `AMExt` | 扩展 | u32 长度前缀 + 字节内容 |

字符串辅助函数要点：

- `str_to_bin_u8`：长度超过 `u8::MAX` 直接 panic
- `str_to_bin_u16`：长度超过 `u16::MAX` 直接 panic，长度按 big-endian 写入
- `bin_to_str_u8` / `bin_to_str_u16`：长度字段缺失或数据不完整返回错误，UTF-8 校验失败返回 `Invalid UTF-8 string data`
- `AMHeaders` 解码使用 `BTreeMap<String, String>` 按 header 数量循环读取 key/value

该序列

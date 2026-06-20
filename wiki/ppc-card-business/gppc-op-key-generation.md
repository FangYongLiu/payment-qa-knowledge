---
title: GPPC OP密钥生成指南
domain: ppc-card-business
kind: wiki_page
slug: gppc-op-key-generation
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:6254e0fb-2391-4859-b312-c64c7fbd2908
tags: []
---

# GPPC OP密钥生成指南

本页说明如何使用 OpenSSL 查看并验证 GPPC OP 场景下 RSA 公钥的模数（Modulus）与指数（Exponent）。

## 适用场景

- 校验 PEM 格式公钥文件（如 `public.pem`）的内容
- 提取 RSA 公钥的 Modulus 与 Exponent，用于密钥配置或对接核对

## 查看公钥命令

使用 OpenSSL 解析 PEM 公钥文件：

```shell
openssl rsa -pubin -in public.pem -text -noout -modulus
```

参数说明：

- `-pubin`：输入文件为公钥
- `-in public.pem`：指定输入文件
- `-text`：以文本形式打印密钥内容
- `-noout`：不输出编码后的密钥
- `-modulus`：额外打印一行连续十六进制的 Modulus

## 输出内容解读

执行后典型输出包含以下字段：

- `RSA Public-Key: (2048 bit)`：表示该公钥为 2048 位 RSA
- `Modulus:`：以冒号分隔的十六进制字节对形式按多行缩进打印模数
  - 例如以 `00:b9:ef:33:89:19:2f:67:b0:61:39:5f:12:7a:2d:...` 开头，以 `...30:95` 结尾
- `Exponent: 65537 (0x10001)`：公钥指数，固定为 `65537`（十六进制 `0x10001`）
- `Modulus=`：将上述模数以单行连续大写十六进制字符串形式再次输出（无冒号分隔），便于直接复制粘贴使用
  - 例如：`B9EF3389192F67B061395F127A2DB81C79ACCD33CB1C8E391C347A7C32C197C4B68D3D2A8B60653AF098C7569A3BE7B04DA6F3AE38DDFA...56D3D9182A1AAB78ADC1B6FBF6769256FA0D2861B02B3095`

## 验证要点

- 确认密钥长度为 `2048 bit`
- 确认 `Exponent` 为 `65537 (0x10001)`
- 使用 `Modulus=` 行的连续十六进制字符串与对端配置进行比对核验

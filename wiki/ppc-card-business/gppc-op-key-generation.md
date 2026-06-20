---
title: GPPC OP密钥生成指南
domain: ppc-card-business
kind: wiki_page
slug: gppc-op-key-generation
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:a8b7e3c3-4035-45a4-88aa-5ec03613577d
tags: []
---

# GPPC OP密钥生成指南

本页说明 GPPC 对接所需 RSA 密钥对的生成方法，以及如何查看公钥信息。

## 生成 RSA 密钥对

使用 OpenSSL 生成私钥与对应公钥，用于 GPPC OP 接入。

## 查看公钥信息

可通过 OpenSSL 命令打印公钥的详细信息（如 `openssl rsa -pubin -text -modulus`），输出包含：

- **RSA Public-Key**：密钥位数，例如 `RSA Public-Key: (1408 bit)`
- **Modulus**：以冒号分隔的十六进制字节对形式逐行展示模数

示例输出片段：

```
RSA Public-Key: (1408 bit)
Modulus:
    00:e0:a8:db:7c:a3:7b:22:00:46:d3:42:17:da:18:
    ca:30:85:61:2f:92:a8:d6:10:19:5e:d4:3f:c0:95:
    2d:17:f5:93:20:2d:3b:7d:09:d9:6d:f1:5f:2a:40:
    2a:fa:47:7c:a5:f4:c7:82:46:a5:52:58:33:6f:3f:
    7a:16:2b:99:ed:b1:df:42:8b:fd:9b:8f:b1:d6:2e:
    cb:0e:a4:d6:5d:87:1d:14:48:62:18:0f:69:3f:80:
    5a:1f:f9:39:d2:05:1b:58:62:14:24:bd:41:5b:ae:
    37:17:c3:b7:52:ec:92:9a:8f:75:30:48:37:23:ed:
    a7:c0:b8:80:3e:84:46:3e:41:63:8d:5d:6c:69:e8:
    fc:38:d8:db:4b:02:50:9d:53:38:36:db:2e:0a:6f:
    9b:e6:d1:5e:fc:a2
```

## 关注要点

- 确认密钥位数是否符合对接要求（示例中为 1408 bit）。
- Modulus 用于 GPPC 对端校验公钥一致性，需完整保留。

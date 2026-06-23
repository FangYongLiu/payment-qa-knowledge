---
title: Botim-PayBy gRPC网关协议定义
domain: channel-integration
kind: wiki_page
slug: botim-payby-grpc-gateway-protocol
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/1072791687
tags: []
---

# Botim-PayBy gRPC网关协议定义

本页定义 Botim 与 PayBy 之间网关通道使用的 gRPC 接口、`ApplicationMessage` 报文结构以及二进制编解码细节。加解密细节见 [[botim-payby-payload-security]]，整体方案背景见 [[botim-payby-server-integration-overview]]。

## gRPC Proto 定义

- package：`at_df`
- service：`DownstreamCaller`
  - `rpc send(DFRequest) returns (google.protobuf.Empty)`：单向下行
  - `rpc call(DFRequest) returns (DFResponse)`：请求/响应

报文：

- `DFRequest { bytes message = 1; }`
- `DFResponse { bytes message = 1; DownstreamStatus status = 2; }`
- `enum DownstreamStatus { OK = 0; ERROR = 1; }`

`message` 字段承载经过二进制编码（再经 AES-GCM 加密）的 `ApplicationMessage`。

## ApplicationMessage 顶层结构

`ApplicationMessage` 字段：

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| `version` | byte | 报文版本号 |
| `id` | String | 每个请求的 Request ID，长度 16 |
| `meta` | Meta | 元数据，见下文 |
| `amp` | String | Application Message Payload（JSON） |

## Meta 字段定义

| 字段 | 含义 | 长度限制 |
| --- | --- | --- |
| `adn` | Application Downstream Name，下游来源 | 最长 127（1 byte 长度前缀） |
| `adm` | Application Downstream Method，被调用方法 | 最长 127（1 byte） |
| `asn` | Application Source Name，请求来源 | 最长 127（1 byte） |
| `asm` | Application Source Method | 最长 127（1 byte） |
| `amt` | Trusty，可放签名等 | 最长 65535（2 bytes） |
| `amf` | Flags，2 bytes，每 bit 一个 flag | Character |
| `amh` | Header（key/value Map） | key < 127（1 byte），value < 65535（2 bytes） |
| `ame` | Application Message Extension，可放任意 text/json | 最长 `Integer.MAX_VALUE`（4 bytes） |
| `amc` | Communication Mode，默认 `ComMode.CALL` | 1 byte |

### Meta → adm

用于指定客户端调用的具体 API，例如 `/personal/v1/bind-customer`。对应业务接口见：

- [[api_personal_bind_customer]] `/personal/v1/bind-customer`
- [[api_personal_login_or_refresh]] `/personal/v1/login-or-refresh`
- [[api_personal_v3_auth_login]] `/personal/v3/auth/login`

### Meta → adh（Header）

| Header Name | Header Value | 示例 |
| --- | --- | --- |
| `partner-id` | Partner ID | `20000000006` |
| `Content-Language` | 语言类型 | `en`, `ar`, `zh` |

### amp（Application Message Payload）

JSON 文本，包含业务字段。示例：

```json
{
  "requestTime": 17691238142134,
  "bizContent": {
    "mobileNumber": "xxxx",
    "uid": "xxx"
  }
}
```

## 二进制编解码规范

`ApplicationMessage` 经过自定义二进制编码后再传输（参考 Rust `ToBinRepr`/`FromBinRepr` 实现）。

### 长度前缀约定

- **u8 长度前缀（≤127 字节）**：`asn`、`asm`、`adn`、`adm`
  - 1 byte 长度 + UTF-8 字节
- **u16 长度前缀（big-endian，≤65535 字节）**：`amt`（AMTrusty）
  - 2 bytes 长度 + UTF-8 字节
- **u32 长度前缀（big-endian）**：`amp`（AMP）
  - 4 bytes 长度 + payload 字节

### 各字段编码

| 字段 | 编码规则 |
| --- | --- |
| `AMVer` | 单字节 |
| `AMID` | 16 字节（UUID bytes） |
| `ASN` / `ASM` / `ADN` / `ADM` | u8 长度 + UTF-8 |
| `AMTrusty` | u16 长度（big-endian）+ UTF-8 |
| `AMP` | u32 长度（big-endian）+ 原始字节 |
| `AMFlag` | 2 字节固定 |

### 解码错误条件

- `AMVer is too short`：剩余 < 1 字节
- `AMID is too short`：剩余 < 16 字节
- `String length field is missing` / `String data is incomplete`：长度前缀或内容不完整
- `Invalid UTF-8 string data`：UTF-8 解码失败
- `AMP length field is missing` / `AMP payload is incomplete`：AMP 长度/正文不完整
- `AMFlag is too short`：剩余 < 2 字节

## 报文安全

`message` 在 gRPC 传输前需经过 AES-256/GCM/NoPadding 加密，密文格式为 `12 bytes nonce + ciphertext`，再 Base64 编码。完整加解密流程与示例代码参见 [[botim-payby-payload-security]]。

## 关联接口

通过该网关调用的 API：

- [[api_personal_bind_customer]] 绑定客户
- [[api_personal_login_or_refresh]] 登录或刷新 Token
- [[api_personal_v3_auth_login]] 客户登录（合并自 `/personal/apply/authToken` 与 `/personal/v2/auth/login`）

反向（PayBy → Botim）调用清单见 [[botim-payby-outbound-apis]]；UID/手机号变更兼容场景见 [[botim-uid-mobile-change-cases]]。

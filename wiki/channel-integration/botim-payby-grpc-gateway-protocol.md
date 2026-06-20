---
title: Botim-PayBy gRPC网关协议规范
domain: channel-integration
kind: wiki_page
slug: botim-payby-grpc-gateway-protocol
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:a01637cc-4974-45c3-b1e9-d194dac7ed1f
tags: []
---

# Botim-PayBy gRPC网关协议规范

本页定义 Botim 与 PayBy 之间 gRPC 网关的 Proto 接口、ApplicationMessage 报文结构、字段约束以及载荷加解密规则，供渠道接入侧实现报文编解码与安全传输。整体方案与背景见 [[botim-payby-server-integration-overview]]，加解密细节见 [[botim-payby-payload-encryption]]。

## gRPC Proto 定义

- package：`at_df`
- service：`DownstreamCaller`
  - `rpc send(DFRequest) returns (google.protobuf.Empty)`
  - `rpc call(DFRequest) returns (DFResponse)`
- `DFRequest`：`bytes message = 1`
- `DFResponse`：
  - `bytes message = 1`
  - `DownstreamStatus status = 2`
  - 枚举 `DownstreamStatus { OK = 0; ERROR = 1; }`

```proto
syntax = "proto3";
import "google/protobuf/empty.proto";
package at_df;

service DownstreamCaller {
  rpc send(DFRequest) returns (google.protobuf.Empty) {}
  rpc call(DFRequest) returns (DFResponse) {}
}
```

## ApplicationMessage 总体结构

请求 `DFRequest.message` 中承载 ApplicationMessage，含以下顶层字段：

- `version` (byte)：报文版本
- `id` (String, 16字节)：每次请求唯一 Request ID
- `meta` (Meta)：元数据
- `amp` (String)：Application Message Payload（JSON）

## Meta 字段定义

| 字段 | 含义 | 长度约束 |
|---|---|---|
| `adn` | Application Downstream Name，下游来源标识 | 最大 127（1 byte 长度前缀） |
| `adm` | Application Downstream Method，被调用的方法 | 最大 127（1 byte） |
| `asn` | Application Source Name，请求来源 | 最大 127（1 byte） |
| `asm` | Application Source Method | 最大 127（1 byte） |
| `amt` | Trusty，可用于签名 | 最大 65535（2 byte） |
| `amf` | Flags，1 bit 1 个标志 | 2 bytes |
| `amh` | Header 键值对 | key ≤127(1B)，value ≤65535(2B) |
| `ame` | Application Message Extension，文本/JSON 任意 | 最大 `Integer.MAX_VALUE`（4 byte） |
| `amc` | Communication Mode，默认 `ComMode.CALL` | 1 byte |

### Meta → adm

用于指示客户端请求的 API，例如 `/personal/v1/bind-customer`。对应业务 API 见：

- [[api_personal_bind_customer]] `/personal/v1/bind-customer`
- [[api_personal_login_or_refresh]] `/personal/v1/login-or-refresh`
- [[api_personal_v3_auth_login]] `/personal/v3/auth/login`

完整 Outbound API 清单参见 [[botim-payby-outbound-apis]]。

### Meta → adh（Header）

| Header Name | Header Value | 示例 |
|---|---|---|
| `partner-id` | Partner ID | `20000000006` |
| `Content-Language` | 语言类型 | `en`, `ar`, `zh` |

## amp 载荷格式

`amp` 为 JSON 字符串，承载具体业务请求/响应内容，例如：

```json
{
  "requestTime": 17691238142134,
  "bizContent": {
    "mobileNumber": "xxxx",
    "uid": "xxx"
  }
}
```

## 二进制编解码规则

ApplicationMessage 各字段按以下二进制布局序列化（参考 Rust 实现）：

- **AMVer**：1 byte
- **AMID**：16 bytes（UUID 原始字节）
- **ASN / ASM / ADN / ADM**：`u8 长度` + UTF-8 字节
- **AMTrusty**：`u16 长度（大端）` + UTF-8 字节
- **AMP**：`u32 长度（大端）` + payload 字节
- **AMFlag**：2 bytes
- **AMHeaders**：
  - `u8` headers 数量
  - 每项：`u8 长度 key` + `u16 长度 value`
- **AMExt**：`u32 长度（大端）` + 字节内容

字符串长度均使用大端字节序（`to_be_bytes`），超长会触发 panic（`exceeds u8::MAX` / `u16::MAX`）。解码侧逐段读取，长度不足时返回错误（如 `AMID is too short`、`String data is incomplete`、`Invalid UTF-8 string data`）。

## 请求安全：Payload 加解密概要

报文整体使用 AES 加密以密文传输，参数：

- Key length：AES-256
- Algorithm：`AES/GCM/NoPadding`
- IV length：16 字符
- IV 拼接在密文之前
- 最终结果使用 Base64 编码

实现常量（Java 示例）：

- `GCM_TAG_LENGTH = 16`
- `GCM_NONCE_LENGTH = 12`
- `ALGORITHM = "AES"`
- `TRANSFORMATION = "AES/GCM/NoPadding"`
- 加密结果格式：`12 bytes nonce + encrypted bytes`

详细加解密代码与流程见 [[botim-payby-payload-encryption]]。

## 关联 API 文档

- Personal 文档入口：`http://sim.intra.test2pay.com/api-doc/sgs-api/personal-sgs-api/`
- 协议承载的核心 API：
  - `/personal/v1/bind-customer` — Bind Customer
  - `/personal/v1/login-or-refresh` — Login or Refresh Token
  - `/personal/v3/auth/login` — Customer Login

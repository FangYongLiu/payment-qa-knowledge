---
id: reference_client_grpc_gateway_integration
object_type: Reference
name: 客户端 gRPC 网关集成规范(Proto / Application Message / HTTP Header)
aliases:
- client-grpc-gateway-integration
- DownstreamCaller
- ApplicationMessage
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:PMDPayment/1073217736; wiki:978e4ed8-87ba-46f5-9435-d326f7c9f637
tags:
- cgs
- grpc
- 网关
- protocol
- http-header
related_services:
- svc_cgs
---

# 客户端 gRPC 网关集成规范(Proto / Application Message / HTTP Header)

> 客户端经 HTTP 网关到内部服务([[svc_cgs]])的 gRPC 转发协议速查:请求流转 + Proto Buffer 报文 + Application Message 结构 + 客户端必须携带的 HTTP Header。QA 联调/构造请求的字典。

## 请求流转
客户端 HTTP 请求经 http gateway 转换为 gRPC 请求并下发到内部服务(cgs),由 cgs 解析 gRPC 请求并构造内部上下文。H5 场景额外存在 Session Authorization 流程。

| 步骤 | 动作 | 说明 | 系统 |
| --- | --- | --- | --- |
| 1.2 gRPC Request | http request → gRPC request | 转发 http header 与 http body 到下游 | http gateway |
| 1.2.1 Parse gRPC request | 解析 gRPC request | 转为内部 context | cgs |

## gRPC Proto 定义
- package:`at_df`;service:`DownstreamCaller`
  - `rpc send(DFRequest) returns (google.protobuf.Empty)` — 单向请求
  - `rpc call(DFRequest) returns (DFResponse)` — 请求-响应
- `DFRequest { bytes message = 1; }`
- `DFResponse { bytes message = 1; DownstreamStatus status = 2; }`,枚举 `OK = 0` / `ERROR = 1`

## Application Message 结构
`DFRequest.message` 的 bytes 内容承载 ApplicationMessage:

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| version | byte | 消息版本 |
| id | String(16) | Request ID |
| meta | Meta | 元数据(见下) |
| amp | String | Application Message Payload(JSON 文本) |

### Meta 字段
| 字段 | 含义 | 长度/约束 |
| --- | --- | --- |
| adn | Application Downstream Name,下游来源标识 | ≤127(1 byte 长度) |
| adm | Application Downstream Method,被调用方法 | ≤127(1 byte 长度) |
| asn | Application Source Name,请求来源 | ≤127 |
| asm | Application Source Method | ≤127 |
| amt | Trusty,可承载签名/client proof | ≤65535(2 bytes 长度) |
| amf | Flags,1 bit 表示一个标志位 | 2 bytes |
| amh | Header(map) | key<127(1 byte),value<65535(2 bytes) |
| ame | Application Message Extension,可放 text/json | ≤`Integer#MAX_VALUE`(4 bytes 长度) |
| amc | Communication Mode | 1 byte,默认 `ComMode.CALL` |

### 关键字段约定
- `meta.adm`:客户端请求的 API,例如 `/personal/v1/bind-customer`。
- `meta.amh`(Header Map)常用项:`partner-id`(如 `20000000006`)、`Content-Language`(`en`/`ar`/`zh`)。
- `meta.amt`:放置 client proof。
- `amp`:JSON 负载,例如:
  ```json
  { "requestTime": 17691238142134, "bizContent": { "mobileNumber": "xxxx", "uid": "xxx" } }
  ```

## 必需的 HTTP Header
| Header | Required | 备注 |
| --- | --- | --- |
| Content-Language | Mandatory | |
| Referer | Mandatory | |
| X-Token | Optional | 仅 authentication API |
| X-Sign | Mandatory | |
| X-Platform | Mandatory | |
| X-Device-Id | Optional | 仅 App |
| X-Sdk-Version | Optional | 仅 App |
| X-Host-App | Optional | 仅 App |
| Host-App-Version | Optional | 仅 App |
| Host-App-Channel | Optional | 仅 PayBy App |
| Utc-Offset-Seconds / X-TZ-Offset | Mandatory | |
| Salt-Key | Optional | 仅属性加密 |
| X-Tmx-Session | Optional | 仅 App |
| X-Ali-Session | Optional | |
| X-TZ-Offset | Mandatory | |
| X-Guard-Token | Optional | 仅 App |
| X-Forwarded-For | Mandatory | 客户端 IP,例如 `210.2.11.52` |
| X-UCID | Optional | 仅 Botim mini-program |
| X-Account-Id | Optional | 仅文件上传 |
| File-Suffix | Optional | 仅文件上传 |
| Business-Tags | Optional | 按风控要求 |

## 大文件上传(保留既有路径,不走标准网关流程)
- `/cgs/api/bigfield/upload`
- `/cgs/api/uploadUn`
- `/cgs/api/upload-encrypt`
- `/cgs/api/v1/file/upload`

## 关联关系
- **所属服务**:[[svc_cgs]](= `related_services`;cgs 为该协议的内部接收端)

---
title: 客户端gRPC网关集成规范
domain: payby-core-systems
kind: wiki_page
slug: client-end-grpc-integration
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/1073217736
tags: []
---

# 客户端gRPC网关集成规范

本页定义客户端经 HTTP 网关到内部服务的 gRPC 转发协议，包括请求流程、Proto Buffer 报文、Application Message 结构以及客户端必须携带的 HTTP Header。

## 请求流程

客户端 HTTP 请求经 http gateway 转换为 gRPC 请求并下发到内部服务（cgs），由 cgs 解析 gRPC 请求并构造内部上下文。

| 步骤 | 动作 | 说明 | 系统 |
| --- | --- | --- | --- |
| 1.2 gRPC Request | 将 http request 转换为 gRPC request | 转发 http header 与 http body 到下游 | http gateway |
| 1.2.1 Parse gRPC request | 解析 gRPC request | 将 gRPC request 转为内部 context | cgs |

H5 场景额外存在 Session Authorization 流程。

## gRPC Proto 定义

- package：`at_df`
- service：`DownstreamCaller`
  - `rpc send(DFRequest) returns (google.protobuf.Empty)`
  - `rpc call(DFRequest) returns (DFResponse)`
- `DFRequest`
  - `bytes message = 1`
- `DFResponse`
  - `bytes message = 1`
  - `DownstreamStatus status = 2`，枚举 `OK = 0`、`ERROR = 1`

## Application Message 结构

报文整体字段：

- `version` (byte)：消息版本
- `id` (String, 16)：每个请求的 Request ID
- `meta` (Meta)：元数据
- `amp` (String)：Application Message Payload，JSON 文本

### Meta 字段

| 字段 | 含义 | 长度/约束 |
| --- | --- | --- |
| `adn` | Application Downstream Name，下游来源标识 | 最大 127（1 byte 长度） |
| `adm` | Application Downstream Method，被调用方法 | 最大 127（1 byte 长度） |
| `asn` | Application Source Name，请求来源 | 最大 127（1 byte 长度） |
| `asm` | Application Source Method | 最大 127（1 byte 长度） |
| `amt` | Trusty，可承载签名等可信信息 | 最大 65535（2 bytes 长度） |
| `amf` | Flags，1 bit 表示一个标志位 | 2 bytes |
| `amh` | Header（map） | key 长度 < 127（1 byte），value 长度 < 65535（2 bytes） |
| `ame` | Application Message Extension，可放 text/json 等任意内容 | 最大 `Integer#MAX_VALUE`（4 bytes 长度） |
| `amc` | Communication Mode | 1 byte，默认 `ComMode.CALL` |

### 关键字段约定

- `meta.adm`：指明客户端请求的 API，例如 `/personal/v1/bind-customer`
- `meta.adh`（Header Map）常用项：
  - `partner-id`：Partner ID，例如 `20000000006`
  - `Content-Language`：语言类型，如 `en`、`ar`、`zh`
- `meta.amt`：放置 client proof
- `amp`：JSON 负载，例如：
  ```json
  {
      "requestTime": 17691238142134,
      "bizContent": {
          "mobileNumber": "xxxx",
          "uid": "xxx"
      }
  }
  ```

## 必需的 HTTP Header

| Header Name | Required |
| --- | --- |
| Content-Language | Mandatory |
| Referer | Mandatory |
| X-Token | Optional，仅 authentication API |
| X-Sign | Mandatory |
| X-Platform | Mandatory |
| X-Device-Id | Optional，仅 App |
| X-Sdk-Version | Optional，仅 App |
| X-Host-App | Optional，仅 App |
| Host-App-Version | Optional，仅 App |
| Host-App-Channel | Optional，仅 PayBy App |
| Utc-Offset-Seconds 或 X-TZ-Offset | Mandatory |
| Salt-Key | Optional，仅属性加密 |
| X-Tmx-Session | Optional，仅 App |
| X-Ali-Session | Optional |
| X-TZ-Offset | Mandatory |
| X-Guard-Token | Optional，仅 App |
| X-Forwarded-For | Mandatory，客户端 IP，例如 `210.2.11.52` |
| X-UCID | Optional，仅 Botim mini-program |
| X-Account-Id | Optional，仅文件上传 |
| File-Suffix | Optional，仅文件上传 |
| Business-Tags | Optional，按风控要求 |

## 大文件上传

大文件上传场景保持原有路径不变，包括：

- `/cgs/api/bigfield/upload`
- `/cgs/api/uploadUn`
- `/cgs/api/upload-encrypt`
- `/cgs/api/v1/file/upload`

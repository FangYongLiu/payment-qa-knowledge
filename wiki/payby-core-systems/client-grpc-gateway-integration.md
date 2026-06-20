---
title: 客户端gRPC网关集成规范
domain: payby-core-systems
kind: wiki_page
slug: client-grpc-gateway-integration
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:978e4ed8-87ba-46f5-9435-d326f7c9f637
tags: []
---

# 客户端gRPC网关集成规范

本页定义客户端通过 HTTP 网关接入内部服务的 gRPC 协议规范，包括请求流转、Proto Buffer 消息结构、Application Message 字段约束以及必需的 HTTP Header 列表。

## 目标

- 实现 gRPC 网关
- 将 gRPC 请求分发到内部服务

## 请求流转

| 步骤 | 动作 | 说明 | 系统 |
|---|---|---|---|
| 1.2 gRPC Request | 将 http 请求转换为 gRPC 请求 | 转发 http header、http body 到下游 | http gateway |
| 1.2.1 Parse gRPC request | 解析 gRPC 请求 | 将 gRPC 请求转换为内部上下文 | cgs |

另需支持 H5 Session Authorization 流程。

## gRPC Protocol 定义

### Proto Buffer Message

```proto
syntax = "proto3";
import "google/protobuf/empty.proto";
package at_df;

service DownstreamCaller {
  rpc send(DFRequest) returns (google.protobuf.Empty) {}
  rpc call(DFRequest) returns (DFResponse) {}
}

message DFRequest {
  bytes message = 1;
}

message DFResponse {
  bytes message = 1;
  DownstreamStatus status = 2;
  enum DownstreamStatus {
    OK = 0;
    ERROR = 1;
  }
}
```

- `send`：单向请求，返回 `google.protobuf.Empty`
- `call`：请求-响应，返回 `DFResponse`
- `DownstreamStatus` 枚举：`OK = 0`、`ERROR = 1`

## Application Message 结构

`DFRequest.message` 的 bytes 内容承载 ApplicationMessage：

| 字段 | 类型 | 说明 |
|---|---|---|
| version | byte | Message Version |
| id | String | Request ID，长度 16 |
| meta | Meta | 元信息（见下） |
| amp | String | Application Message Payload（JSON） |

### Meta 字段

| 字段 | 类型 | 说明 / 长度限制 |
|---|---|---|
| adn | String | Application Downstream Name，标识下游来源；最大长度 127（1 byte） |
| adm | String | Application Downstream Method，标识被调用方法；最大长度 127（1 byte） |
| asn | String | Application Source Name，标识请求来源；最大长度 127（1 byte） |
| asm | String | Application Source Method；最大长度 127（1 byte） |
| amt | String | Trusty，最大长度 65535（2 bytes）；可承载签名 |
| amf | Character | Flags，2 bytes，1 bit 表示一个 flag |
| amh | Map<String,String> | Header，key 长度 < 127（1 byte），value 长度 < 65535（2 bytes） |
| ame | String | Application Message Extension，最大长度 `Integer#MAX_VALUE`（4 bytes），可为 text/json |
| amc | ComMode | Communication Mode，1 byte，默认 `ComMode.CALL` |

### Meta.adm

用于指示客户端请求的 API。例如：`/personal/v1/bind-customer`。

### Meta.adh（Header）

| Header Name | Header Value | 示例 |
|---|---|---|
| partner-id | Partner ID | 20000000006 |
| Content-Language | Lang Type | en, ar, zh |

### Meta.amt

承载客户端 proof（签名/凭证）。

### amp（Payload）

JSON 格式的消息体，示例：

```json
{
  "requestTime": 17691238142134,
  "bizContent": {
    "mobileNumber": "xxxx",
    "uid": "xxx"
  }
}
```

## Required HTTP Header

| Header Name | 是否必需 | 备注 |
|---|---|---|
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
| Utc-Offset-Seconds 或 X-TZ-Offset | Mandatory | |
| Salt-Key | Optional | 仅属性加密时 |
| X-Tmx-Session | Optional | 仅 App |
| X-Ali-Session | Optional | |
| X-TZ-Offset | Mandatory | |
| X-Guard-Token | Optional | 仅 App |
| X-Forwarded-For | Mandatory | 客户端 IP，例如 `210.2.11.52` |
| X-UCID | Optional | 仅 Botim mini-program |
| X-Account-Id | Optional | 仅文件上传 |
| File-Suffix | Optional | 仅文件上传 |
| Business-Tags | Optional | 按风控要求 |

## 大文件上传

保留以下既有路径，不走标准网关流程：

- `/cgs/api/bigfield/upload`
- `/cgs/api/uploadUn`
- `/cgs/api/upload-encrypt`
- `/cgs/api/v1/file/upload`

---
title: PayBy客户端集成请求调用链路
domain: payby-open-api
kind: wiki_page
slug: payby-client-integration-request-flow
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:d903dc69-6256-4b23-a1ea-403e94afa2d9
tags: []
---

# PayBy客户端集成请求调用链路

本页描述用户调用 PayBy API 时，请求在 `http-gateway`、`cgs-grpc` 和 `payby server` 之间的协议桥接与时序流转，整体链路为 **HTTP → gRPC → Dubbo**。

## 参与组件

- **user**：API 调用方（客户端）
- **http-gateway**：对外 HTTP 入口，负责协议翻译
- **cgs-grpc**：gRPC 服务，负责解析请求并转发
- **payby server**：后端业务服务，通过 Dubbo 暴露能力

## 请求时序

1. **1 Request some apis**：user 通过 HTTP 调用 http-gateway 暴露的 API
2. **1.1 Translate to gRPC request**：http-gateway 内部将 HTTP 请求翻译为 gRPC 请求
3. **1.2 gRPC request**：http-gateway 以 gRPC 协议调用 cgs-grpc
4. **1.2.1 Parse gRPC request**：cgs-grpc 内部解析 gRPC 请求
5. **1.2.2 Dubbo request**：cgs-grpc 通过 Dubbo 调用 payby server

## 响应回传

响应沿原路径反向逐层回传：

1. **1.2.3 Response**：payby server → cgs-grpc
2. **1.3 Response**：cgs-grpc → http-gateway
3. **1.4 Response**：http-gateway → user

## 协议桥接小结

整条链路体现了三段式协议转换：

- user ↔ http-gateway：**HTTP**
- http-gateway ↔ cgs-grpc：**gRPC**
- cgs-grpc ↔ payby server：**Dubbo**

http-gateway 承担 HTTP→gRPC 的翻译职责，cgs-grpc 承担 gRPC→Dubbo 的桥接职责。

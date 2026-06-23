---
title: PayBy客户端API调用链路说明
domain: payby-open-api
kind: wiki_page
slug: payby-client-integration-call-flow
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:8db10392-fd7c-456f-ae5c-ac4c590ae7ab
tags: []
---

# PayBy客户端API调用链路说明

本页描述客户端（user）发起一次 PayBy API 调用时，请求与响应在 `http-gateway`、`cgs-grpc`、`payby server` 之间的流转过程。

## 参与方

- **user**：发起 API 调用的客户端。
- **http-gateway**：对外的 HTTP 入口网关，负责将 REST 风格请求转换为 gRPC 请求。
- **cgs-grpc**：gRPC 服务层，负责解析 gRPC 请求并以 Dubbo 方式调用后端服务。
- **payby server**：后端业务服务，处理实际业务逻辑（通过 Dubbo 暴露）。

## 请求链路（正向）

调用顺序按时序图编号如下：

1. **1 Request some apis**：user → http-gateway，发起 API 请求。
2. **1.1 Translate to gRPC request**：http-gateway 自身处理，将请求转换为 gRPC 请求。
3. **1.2 gRPC request**：http-gateway → cgs-grpc，转发 gRPC 请求。
4. **1.2.1 Parse gRPC request**：cgs-grpc 自身处理，解析收到的 gRPC 请求。
5. **1.2.2 Dubbo request**：cgs-grpc → payby server，以 Dubbo 调用后端服务。

## 响应链路（反向）

响应沿调用栈逐层回传：

- **1.2.3 Response**：payby server → cgs-grpc。
- **1.3 Response**：cgs-grpc → http-gateway。
- **1.4 Response**：http-gateway → user。

## 协议转换要点

整条链路涉及三种协议形态的转换：

- **HTTP（REST）** 入口：user ↔ http-gateway。
- **gRPC**：http-gateway ↔ cgs-grpc。
- **Dubbo**：cgs-grpc ↔ payby server。

每一跳节点在处理期间均处于激活状态，请求由 http-gateway 完成 HTTP→gRPC 翻译，由 cgs-grpc 完成 gRPC→Dubbo 翻译，最终到达 payby server。

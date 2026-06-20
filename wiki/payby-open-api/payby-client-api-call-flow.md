---
title: PayBy客户端API调用链路
domain: payby-open-api
kind: wiki_page
slug: payby-client-api-call-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:28b4be2d-315d-499c-a641-7424739a22f4
tags: []
---

# PayBy客户端API调用链路

本页描述PayBy客户端发起API请求后，经由 http-gateway、cgs-grpc 转发至 payby server 的协议转换与响应回传完整链路。

## 参与角色

调用链路涉及以下四个角色（由客户端到后端依次排列）：

- **user**：发起API调用的客户端（用户）
- **http-gateway**：HTTP接入网关
- **cgs-grpc**：gRPC转换服务
- **payby server**：后端业务服务

## 请求与响应流程

整体调用按编号顺序进行，请求逐层向后转发，响应原路返回。

### 请求阶段

- **1. Request some apis**：user 向 http-gateway 发起 API 请求
- **1.1 Translate to gRPC request**：http-gateway 内部将 HTTP 请求翻译为 gRPC 请求
- **1.2 gRPC request**：http-gateway 将 gRPC 请求转发至 cgs-grpc
- **1.2.1 Parse gRPC request**：cgs-grpc 内部解析 gRPC 请求
- **1.2.2 Dubbo request**：cgs-grpc 将请求转换为 Dubbo RPC 调用，发往 payby server

### 响应阶段

响应沿原链路反向返回：

- **1.2.3 Response**：payby server → cgs-grpc
- **1.3 Response**：cgs-grpc → http-gateway
- **1.4 Response**：http-gateway → user

## 协议转换要点

链路中存在两次协议转换，分别由两个中间组件承担：

- **http-gateway**：负责 HTTP ↔ gRPC 协议互转
- **cgs-grpc**：负责 gRPC ↔ Dubbo 协议互转

最终业务处理由 payby server 通过 Dubbo 协议接收并返回结果。

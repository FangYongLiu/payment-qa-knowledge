---
title: Botim gRPC请求处理时序
domain: channel-integration
kind: wiki_page
slug: botim-grpc-request-processing-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:a568cec9-2bcf-4a35-b6cd-0a493e9f90e1
tags: []
---

# Botim gRPC请求处理时序

本页描述 Botim 4.0.1 中一次 gRPC 请求从入口 `BotimGrpcServiceImpl` 到响应写回的内部调用时序。

## 参与者

按调用顺序，涉及四个组件：

- `BotimGrpcServiceImpl`：gRPC 入口
- `ReceiveOrderService`：请求编排
- `AppService`：业务逻辑处理
- `WriteResponseAssist`：响应写回

## 调用时序

### 1. 入口处理（BotimGrpcServiceImpl）

入口完成请求的前置处理，均为自调用：

1. `check param`：参数校验
2. `deserialize ApplicationMessage`：反序列化 `ApplicationMessage`
3. `processRequest`：委托给 `ReceiveOrderService`

### 2. 请求编排（ReceiveOrderService）

`processRequest` 内部按以下顺序执行：

- 3.1 `check api config`：API 配置校验（自调用）
- 3.2 `doService`：调用 `AppService` 执行业务逻辑
- 3.3 `get service response`：从 `AppService` 返回业务结果（返回箭头）
- 3.4 `encrypt response`：响应加密（自调用）
- 3.5 `transformResponse`：响应转换（自调用）
- 3.6 `write grpc response`：交由 `WriteResponseAssist` 写回 gRPC 响应

## 备注

- 除 3.3 为返回（虚线）外，其余步骤均为同步调用。
- 时序图中未描绘错误或分支处理路径。

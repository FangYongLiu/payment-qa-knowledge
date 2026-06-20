---
title: Botim 4.0.1 gRPC请求处理时序
domain: fund-out-transfer
kind: wiki_page
slug: botim-4-0-1-grpc-request-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:f74980cf-3af5-4747-be1e-a6b3b7dc4605
tags: []
---

# Botim 4.0.1 gRPC请求处理时序

本页记录 Botim 4.0.1 中一次 gRPC 订单请求从入口校验到响应写回的内部调用时序（happy-path，不含异常/分支）。

## 参与者

按调用顺序自左至右：

1. `BotimGrpcServiceImpl` — gRPC 入口
2. `ReceiveOrderService` — 订单接收与编排
3. `AppService` — 业务逻辑执行
4. `WriteResponseAssist` — gRPC 响应写回

## 调用时序

1. `check param` — `BotimGrpcServiceImpl` 自调用，校验入参。
2. `deserialize ApplicationMessage` — `BotimGrpcServiceImpl` 自调用，反序列化 `ApplicationMessage`。
3. `processRequest` — `BotimGrpcServiceImpl` → `ReceiveOrderService`，移交请求处理。
   - 3.1 `check api config` — `ReceiveOrderService` 自调用，检查 API 配置。
   - 3.2 `doService` — `ReceiveOrderService` → `AppService`，执行业务处理。
   - 3.3 返回 — `AppService` → `ReceiveOrderService`（dashed return）。
   - 3.4 `encrypt response` — `ReceiveOrderService` 自调用，加密响应。
   - 3.5 `transformResponse` — `ReceiveOrderService` 自调用，转换响应结构。
   - 3.6 `write grpc response` — `ReceiveOrderService` → `WriteResponseAssist`，写回 gRPC 响应。

## 流程要点

- 入口职责：`BotimGrpcServiceImpl` 仅负责参数校验、`ApplicationMessage` 反序列化，然后下沉到 `ReceiveOrderService`。
- 编排职责：`ReceiveOrderService` 负责 API 配置校验、业务调用、响应加密与转换、响应写回的整体编排。
- 业务执行：实际业务逻辑由 `AppService.doService` 承担。
- 响应写回：统一由 `WriteResponseAssist` 完成 gRPC 层的响应输出。
- 该时序为单一线性 happy-path，未描述错误处理、备选分支或循环。

## 业务域

- domain = `fund-out-transfer`

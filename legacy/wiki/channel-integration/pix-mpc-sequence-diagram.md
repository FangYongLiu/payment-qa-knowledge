---
title: Pix MPC扫码支付流程时序图
domain: channel-integration
kind: wiki_page
slug: pix-mpc-sequence-diagram
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:9c9602f5-5327-4eb3-8d47-40fb3ffd2b4a
tags: []
---

# Pix MPC扫码支付流程时序图

本页描述 Pix 渠道 MPC（Merchant Presented Code，商户呈现码）扫码支付场景下，从用户扫码到查询交易结果的端到端调用时序。

## 参与方

- **User**：发起扫码与确认操作的终端用户
- **wallet**：钱包客户端
- **cgs**：网关服务，对外暴露 `/pix/mpc/v1/*` 接口
- **pix**：Pix 业务服务
- **pix-channel**：Pix 渠道层，承载 `MpcFacade` 接口

## 整体流程

时序按用户交互划分为四个阶段：扫码解析、确认交易信息、支付处理、查询结果。

### 1. 扫码（scan）

用户扫码后，wallet 依次完成获取规则、本地匹配、解析二维码与展示交易信息：

1. `wallet → cgs`：`/pix/mpc/v1/get-rules`
   - `cgs → pix → pix-channel`：`MpcFacade.getMatchRules`
2. `wallet` 自身执行 **match rule**（本地规则匹配）
3. `wallet → cgs`：`/pix/mpc/v1/parse`
   - `cgs → pix → pix-channel`：`MpcFacade#parseCode`
4. `wallet` 自身执行 **show trade information**（向用户展示交易信息）

### 2. 确认交易信息（confirm trade information）

用户确认后，wallet 触发创建交易：

- `wallet → cgs`：`/pix/mpc/v1/create-trade`
  - `cgs → pix → pix-channel`：`MpcFacade#createTrade`

### 3. 支付处理（payment process）

用户在 wallet 内完成支付处理流程（本时序图未展开内部细节）。

### 4. 展示交易结果（show trade result）

wallet 查询最终交易结果并展示给用户：

- `wallet → cgs`：`/pix/mpc/v1/query-trade`
  - `cgs → pix → pix-channel`：`MpcFacade#queryTrade`

## 接口与 Facade 方法对应关系

| cgs 接口 | pix-channel 方法 |
|---|---|
| `/pix/mpc/v1/get-rules` | `MpcFacade.getMatchRules` |
| `/pix/mpc/v1/parse` | `MpcFacade#parseCode` |
| `/pix/mpc/v1/create-trade` | `MpcFacade#createTrade` |
| `/pix/mpc/v1/query-trade` | `MpcFacade#queryTrade` |

## 调用链路特征

- 所有外部请求均经由 `wallet → cgs → pix → pix-channel` 的四层调用路径。
- `cgs` 到 `pix` 之间为内部转发调用，时序图中未单独标注方法名。
- `pix-channel` 通过统一的 `MpcFacade` 暴露 MPC 场景所需的四个能力：规则获取、码解析、创建交易、查询交易。

---
title: NymCard卡片充值(Loading)时序流程
domain: ppc-card-business
kind: wiki_page
slug: nymcard-card-loading-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:09a3d1b3-7ccd-4a0b-bce4-89683d63d5ad
tags: []
---

# NymCard卡片充值(Loading)时序流程

本页描述持卡人(Cardholder)发起卡片充值，经 Client 中转调用 NymCard 完成预充值余额校验与入账的端到端调用时序。

## 参与方(Lifelines)

- **Cardholder**：发起充值的持卡人(actor)。
- **Client**：业务客户端，负责接收充值请求并调用 NymCard。
- **NymCard**：卡片发行/账务系统，负责余额检查与入账。

## 时序步骤

按层级编号(1, 1.1, 1.2, 2, 3, 3.1, 3.2, 3.3)从上到下执行：

1. **loading**：Cardholder → Client，同步调用，发起充值。
   - 1.1 **loading channel process**：Client 自调用，处理充值渠道流程。
   - 1.2 Client → Cardholder，返回(return)。
2. **loading**：Client 自调用，再次激活 Client(进入对接 NymCard 的阶段)。
3. **load**：Client → NymCard，同步调用，触发 NymCard 侧的充值动作。
   - 3.1 **check pre funding balance**：NymCard 自调用，校验预充值余额。
   - 3.2 **do credit**：NymCard 自调用，执行入账(credit)，包含嵌套激活。
   - 3.3 NymCard → Client，返回(return)。

## 调用约定与图示说明

- 实线箭头(实心三角箭头)：同步调用(synchronous call)。
- 虚线箭头(开口箭头)：返回消息(return)。
- 生命线上的矩形：激活/执行区段(activation/execution occurrence)。
- 层级编号：表示调用的嵌套与顺序关系。

## 流程要点

- 充值由 Cardholder 触发，Client 先在本地完成 *loading channel process* 后即向 Cardholder 返回，再异步/后续地与 NymCard 交互。
- NymCard 侧入账前必须先执行 *check pre funding balance*，通过后再 *do credit*。
- 来源：wiki 页面 `pcbs-RA-2406-Nublo-Deprecated`(已废弃标记，仅作流程参考)。

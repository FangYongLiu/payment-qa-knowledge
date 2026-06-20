---
title: PCBS RA-2406 Nublo卡片Loading流程(已废弃)
domain: ppc-card-business
kind: wiki_page
slug: pcbs-ra-2406-nublo-deprecated
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:89086c7e-9ebd-4ff2-a4d6-a4654cbef082
tags: []
---

# PCBS RA-2406 Nublo卡片Loading流程(已废弃)

> ⚠️ 本页面描述的流程为**已废弃**版本，仅作历史参考。

本页基于 UML 时序图说明 NymCard 卡片 Loading 流程中持卡人、Client、NymCard、PayBy 四方的交互关系。

## 参与方

- **Cardholder**：持卡人，流程发起者
- **Client**：客户端，承担 loading channel 处理逻辑
- **NymCard**：卡片服务方，执行 load 动作
- **PayBy**：资金方，提供 pre funds 划拨

## 时序流程

时序图整体分为两个阶段：Client 内部的 loading channel 处理，以及对 NymCard 的 load 调用。

### 阶段一：Loading 发起与 channel 处理

1. **1: loading** — Cardholder 向 Client 发起 loading 请求
2. **1.1: loading channel process** — Client 内部自调用，处理 loading channel
3. **1.2:** — Client 向 Cardholder 返回结果（dashed return）

### 阶段二：Load 执行与资金划拨

4. **2: loading** — Client 自调用，进入 load 执行环节
5. **3: load** — Client 调用 NymCard 执行 load
6. **3.1: move pre funds** — NymCard 调用 PayBy 划拨 pre funds
7. **3.2:** — PayBy 向 NymCard 返回结果（dashed return）
8. **3.3:** — NymCard 向 Client 返回结果（dashed return）

## 交互说明

- **实线箭头**：同步调用（synchronous call）
- **虚线箭头**：返回（return）
- **Activation bar**：Client 出现两段独立激活区间，NymCard 与 PayBy 各有一段激活区间，对应其在流程中的处理时段。

## 流程要点

- 持卡人不直接与 NymCard / PayBy 交互，全部通过 Client 中转。
- Client 在响应持卡人之后，才发起对 NymCard 的 load 调用（两段 activation 分离）。
- 资金划拨由 NymCard 调用 PayBy 完成 `move pre funds`，结果逐层向上返回至 Client。

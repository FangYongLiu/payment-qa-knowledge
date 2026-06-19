---
title: Chargeback 端到端处理流程总览
domain: chargeback
kind: wiki_page
slug: chargeback-process-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:4ad39c53-fb2e-43b6-bfb5-310fd4ae19d7
tags: []
---

# Chargeback 端到端处理流程总览

本页梳理 Chargeback 业务从文件上传到数据有效性匹配的 7 阶段处理流程，呈现各阶段的输入、关键操作与依赖数据表。完整端到端视角参见 [[flow_chargeback_processing]]，业务域定义参见 [[domain_chargeback]]。

## 流程阶段总览

Chargeback 处理共分为 7 个阶段，从原始文件进入到最终数据落库匹配：

1. 上传文件
2. 解析文件
3. 检查数据是否存在
4. 数据结构化
5. 数据有效性匹配链路
6. （后续阶段）
7. （后续阶段）

## Stage 1 — 上传文件

- 支持的文件类型：`VISA`、`MASTERCARD`、`MAGNATI`、`CKO-HISTORY`
- 用户选择对应的文件类型并上传

## Stage 2 — 解析文件

- 根据文件类型获取对应的处理器
- 解析原始文件
- 生成对应的文件模型集合

## Stage 3 — 检查数据是否存在

- 通过 `ARN` 检查数据是否已存在
- 已存在数据：更新状态，更新内容需根据对应的处理器进行判断

## Stage 4 — 数据结构化

- 将对应的文件模型数据转换成 chargeback 模型
- chargeback 模型的 `valid` 字段初始设置为 `0`

## Stage 5 — 数据有效性匹配链路

通过多种匹配键依次进行有效性校验与数据补全：

### 通过 instOrderNo 匹配
- `cmf.tt_inst_order`：确认订单是否存在
- `grc.t_payment_event`：补充交易数据

### 通过 arn 匹配
- `reconciliation.t_clear_flow`：确认是否存在
- `cmf.tt_inst_order`：获取支付订单号
- `grc.t_payment_event`：补充交易数据

### 通过 authCode 匹配
- `reconciliation.t_clear_flow`：确认是否存在 `inst_seq_no`
- `cmf.tt_inst_order`：获取支付订单号
- `grc.t_payment_event`：补充交易数据

### 通过 arn 匹配（清算项）
- `mchtsettle.t_clearing_item`：检查是否存在

---
title: WPS SIF与PAF公司类型差异
domain: wps-payroll
kind: wiki_page
slug: wps-sif-vs-paf
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2272428082
tags: []
---

# WPS SIF与PAF公司类型差异

WPS 产品根据 `bps.t_corporate.process_type` 区分两类公司：**SIF**（默认完整产品）与 **PAF**（仅作为发薪通道的变体）。两者在发薪流程、发票模块、公司结构上有本质差异。

## 区分字段

- 字段：`bps.t_corporate.process_type`
- 取值：`SIF` / `PAF`

## SIF（默认产品）

- 默认的端到端产品形态
- **门户发薪**：企业通过 WPS portal 发起并审批 payroll
- **发票模块**：启用 invoice / billing（参见 [[wps-data-map]] 中 `t_corp_invoice_config`、`t_corp_invoice` 等表）
- 走完整的 [[wps-key-actors]] 协作链路（YSE / PPC / CBUAE / TradeII）

## PAF（变体）

将我们仅作为**发薪通道**使用，主要差异：

- **无门户发薪**：企业不通过 WPS portal 触发发薪
- **无发票模块**：不使用 invoice / billing 配置
- **线下结算**（offline settlement）
- **YSE 驱动发薪**：发薪由 YSE 侧驱动，而非企业门户
- **父/子公司结构**（parent / sub-company）
- 专用数据表：`bps.t_payroll_paf` / `t_payroll_paf_detail`（与 SIF 的 `t_payroll_source` / `_bulk` / `_data` 等区分，详见 [[wps-data-map]]）

## 速查对照

| 维度 | SIF | PAF |
|---|---|---|
| 门户发薪 | ✅ | ❌ |
| 发票模块 | ✅ | ❌ |
| 结算方式 | 在线（TradeII 等） | 线下 |
| 发薪驱动方 | 企业门户 | YSE |
| 公司结构 | 单公司 | 父/子公司 |
| Payroll 表 | `t_payroll_source` / `_bulk` / `_data` 等 | `t_payroll_paf` / `_detail` |

## 相关

- 业务域：[[domain_wps_payroll]]
- 总览与文档划分：[[wps-knowledge-base-overview]]
- 参与方与系统角色：[[wps-key-actors]]

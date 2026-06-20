---
title: WPS关键参与方与系统角色
domain: wps-payroll
kind: wiki_page
slug: wps-key-actors
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2272428082
tags: []
---

# WPS关键参与方与系统角色

本页梳理 WPS 业务中涉及的外部合作方与内部系统，明确各自职责以及相互之间的调用/交互方式。完整业务全景见 [[wps-knowledge-base-overview]]。

## YSE
- 第三方合作伙伴，是 WPS 对外的核心通道。
- 负责生成/上传央行文件，并对外提供一系列 API：`CSPREG`、`WPSCSR`、`WPSSAL`、`BPSLS` 等。
- 持有**卡状态**（activatable / suspended / closed）。
- 所有对 YSE 的调用一律经 PPC 转发，YSE 不直接对接央行。

## PPC
- 内部转发服务，承担"所有与 YSE 的交互"的统一出入口。
- 业务里说"调用某个 YSE API"实际上等价于"通过 PPC 调用"。
- 同时承载虚拟卡数据：`ppc.t_virtual_card` 是卡管理使用的虚拟卡数据表（proxy / CVV / state 等，见 [[wps-data-map]]）。

## CBUAE（UAE 央行）
- 文件交换模型中的 **WPS** 节点。
- 与 CBUAE 的文件交换**只**通过我们自有的 SFTP 通道完成。
- YSE 不会直接连到 CBUAE。

## TradeII
- 内部交易服务，负责实际的资金划拨执行。
- 典型场景：company pool → Payby pool 的资金移动。
- 在创建薪资（Direct Transfer / WPS 出金）链路中由 YSE/TradeII 协同执行。

## Basis
- 内部员工/运营平台。
- 主要用途：
  - 商户与员工的审核（公司注册审核、Add Employee 审核）。
  - 发票/计费配置（`Pay Now` / `Pay Monthly`）。
  - 加解密能力，例如解密卡 CVV。

## 交互关系速览
- 商户/员工接入侧：商户门户 / Botim App → 内部业务系统 → **PPC** → **YSE** → **CBUAE**（仅文件交换走 SFTP）。
- 资金执行侧：内部业务系统 → **TradeII**（内部资金划转）/ 经 PPC → YSE（出金通道）。
- 运营审核与配置：**Basis**（公司/员工审核、Invoice 配置、CVV 解密等）。
- 卡状态归属：由 YSE 维护，应用侧通过 PPC 同步并落库到 `ppc.t_virtual_card`。

## 关联阅读
- 公司维度的产品差异（端到端 vs 仅作出金通道）见 [[wps-sif-vs-paf]]。
- 各参与方对应的数据落地位置见 [[wps-data-map]]。
- 业务域定义见 [[domain_wps_payroll]]。

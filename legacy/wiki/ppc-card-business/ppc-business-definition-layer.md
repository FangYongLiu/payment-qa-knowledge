---
title: PPC业务定义层总览
domain: ppc-card-business
kind: wiki_page
slug: ppc-business-definition-layer
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2134442046
tags: []
---

# PPC业务定义层总览

业务定义层是 [[domain_ppc_card_business]] 知识库的根基层，用于让人和 AI"听懂"PPC 业务；如果术语和流程在此层未对齐，后续的规则、接口、用例都会跑偏。

## 本层用途

- 统一 PPC 卡业务的语言与流程认知
- 作为其他所有层（规则、接口、用例等）的前提依据

## 内容范围

本层应覆盖以下主题：

- **卡产品矩阵**：列出全部卡产品的差异，包括发卡条件、币种、限额、目标用户、卡组织
- **卡生命周期状态机**：每个状态的含义、合法转换、触发条件
- **账户模型**：卡 vs 钱包 vs 多币种子账户 的对应关系
- **术语词典**：卡组织 / 支付 / 合规相关的所有术语
- **业务主流程图**：开卡、激活、消费授权、清算入账、退款、退单、销卡的端到端流程

## 数据来源

- PRD 文档（PPC 项目下所有 PRD）
- 系统设计文档（卡平台、清结算、账务）
- 卡组织标准文档（Mastercard / Jaywan）

## 维护责任

- **主负责人**：Jianfei Wang
- **内容贡献**：待指定
- **当前状态**：骨架（待补充），创建于 2026-05-04

## 子页索引

具体子页见左侧页面树。

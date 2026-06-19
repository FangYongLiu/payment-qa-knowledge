---
title: PPC 业务定义层总览
domain: ppc-card-business
kind: wiki_page
slug: ppc-business-definition-layer
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:20617da5-8195-48ec-8506-f47a8e401839
tags: []
---

# PPC 业务定义层总览

PPC 业务定义层是知识库最底层的"语言对齐层"，用于让人和 AI 能够听懂 PPC 卡业务；术语和流程在这一层对齐之后，规则、接口、用例等其他层才能基于一致的认知展开。

## 本层用途

- 是其他所有层的前提
- 如果术语和流程没有在此对齐，后续的规则、接口、用例都会跑偏

## 应包含的内容

- **卡产品矩阵**：列出全部卡产品的差异（发卡条件、币种、限额、目标用户、卡组织）
- **卡生命周期状态机**：每个状态的含义、合法转换、触发条件
- **账户模型**：卡 vs 钱包 vs 多币种子账户 的对应关系
- **术语词典**：卡组织 / 支付 / 合规相关的所有术语
- **业务主流程图**：开卡、激活、消费授权、清算入账、退款、退单、销卡的端到端流程

## 数据来源

- PRD 文档（PPC 项目下所有 PRD）
- 系统设计文档（卡平台、清结算、账务）
- 卡组织标准文档（Mastercard / Jaywan）

## 维护责任人

- 主负责人：Jianfei Wang
- 内容贡献：待指定

## 元信息

- 创建时间：2026-05-04
- 状态：骨架（待补充）
- 子页：见左侧页面树

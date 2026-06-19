---
id: domain_ppc_card_business
object_type: Domain
domain: ppc-card-business
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: confluence:AQ/2134442046
tags:
- PPC
- 业务定义层
- 卡业务
subdomain: null
module: null
sensitivity: normal
name: PPC卡业务域
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述

PPC卡业务域属于业务定义层（创建于 2026-05-04，维护人：Jianfei Wang，状态：骨架待补充）。该层用途是让人和 AI "听懂" PPC 业务，是其他所有层的前提——如果术语和流程没对齐，后面的规则、接口、用例都会跑偏。

## 覆盖范围

本业务域覆盖 PPC 卡产品的端到端业务，包括：开卡、激活、消费授权、清算入账、退款、退单、销卡。

业务定义层应包含的内容：

- **卡产品矩阵**：列出全部卡产品的差异（发卡条件、币种、限额、目标用户、卡组织）
- **卡生命周期状态机**：每个状态的含义、合法转换、触发条件
- **账户模型**：卡 vs 钱包 vs 多币种子账户 的对应关系
- **术语词典**：卡组织/支付/合规相关的所有术语
- **业务主流程图**：开卡、激活、消费授权、清算入账、退款、退单、销卡的端到端流程

## 关键服务/流程

端到端业务主流程：

1. 开卡
2. 激活
3. 消费授权
4. 清算入账
5. 退款
6. 退单
7. 销卡

涉及的核心模型：卡产品矩阵、卡生命周期状态机、账户模型（卡 / 钱包 / 多币种子账户）。

数据来源：
- PRD 文档（PPC 项目下所有 PRD）
- 系统设计文档（卡平台、清结算、账务）
- 卡组织标准文档（Mastercard / Jaywan）

## QA 关注点

- 术语与流程对齐：业务定义层是其他所有层的前提，术语和流程未对齐会导致规则、接口、用例偏差。
- 卡产品矩阵覆盖度：发卡条件、币种、限额、目标用户、卡组织等差异是否完整。
- 卡生命周期状态机：每个状态含义、合法转换、触发条件需明确。
- 账户模型映射：卡 vs 钱包 vs 多币种子账户的对应关系。
- 卡组织合规：Mastercard / Jaywan 标准文档对齐。
- 当前状态为"骨架（待补充）"，内容贡献人待指定，主负责人 Jianfei Wang。

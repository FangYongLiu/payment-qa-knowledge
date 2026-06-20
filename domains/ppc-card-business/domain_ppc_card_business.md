---
id: domain_ppc_card_business
object_type: Domain
domain: ppc-card-business
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:AQ/2167636024
tags:
- business-definition
- card-product
- layer-1
subdomain: null
module: null
sensitivity: normal
name: PPC卡业务域
aliases: []
related_services: []
related_tables:
- t_card_bin
related_scenarios:
- salary-card-mono-cobadge-overview
related_logs: []
related_requirements: []
related_failures: []
---

## 概述

PPC卡业务域属于业务定义层（创建于 2026-05-04，维护人：Jianfei Wang，状态：骨架待补充）。该层用途是让人和 AI "听懂" PPC 业务，是其他所有层的前提——如果术语和流程没对齐，后面的规则、接口、用例都会跑偏。

随 Salary Card Mono-badge & Co-badge PRD（2026-05-13 review）落地，本域卡产品矩阵从 "TBD" 转为已覆盖：新增 Salary Card × Jaywan Mono 与 Salary Card × MC×Jaywan Co-badge 两个 program，CBUAE Mandate 截止 2026-03-31。

## 覆盖范围

本业务域覆盖 PPC 卡产品的端到端业务，包括：开卡、激活、消费授权、清算入账、退款、退单、销卡。

业务定义层应包含的内容：

- **卡产品矩阵**（KB id `2134179950`）：列出全部卡产品的差异（发卡条件、币种、限额、目标用户、卡组织）
  - Salary Card × Jaywan 行：原标 "待确认 TBD"，PRD 落地后改为 ✅，含 Mono + Co-badge 两个 program
  - Salary Card × Mastercard 行：✅（Co-badge 中 MC 分支）
- **卡生命周期状态机**（KB id `2133393518`）：每个状态的含义、合法转换、触发条件
- **账户模型**：卡 vs 钱包 vs 多币种子账户 的对应关系
- **术语词典**：卡组织/支付/合规相关的所有术语（CAA / CPV / IHC / IPM / MIP / UAESWITCH / proxy_no / NARADA / SVF / BPS 等待补全）
- **业务主流程图**（KB id `2133196989`）：开卡、激活、消费授权、清算入账、退款、退单、销卡的端到端流程

新增 program 范围：

- **Salary Card Jaywan Mono**：PPC 托管，YSE 管理，EDC 印卡，Botim 用户端；仅支持 AED 国内交易，国际硬拒
- **Salary Card MC×Jaywan Co-badge**：Mastercard Prepaid Gold BIN + Jaywan onboard，AED 走 Jaywan / FX 走 MC
- 新 product code：`SALCOB`（Co-badge）/ `SALMOB`（Mono），plastic code `STDPLS*`
- `t_card_bin` 表新增 `product_code` 字段以区分双 scheme 路由

## 关键服务/流程

端到端业务主流程：

1. 开卡
2. 激活
3. 消费授权（Salary Card 域内五段式：Acquirer→UAESWITCH→Jaywan→Botim/YSE→PPC；国际跨境走 Mastercard 既有框架）
4. 清算入账（Co-badge 新 ledger：jaywan pre-settlement / Jaywan Pending / MC Pending）
5. 退款
6. 退单
7. 销卡

涉及的核心模型：卡产品矩阵、卡生命周期状态机、账户模型（卡 / 钱包 / 多币种子账户）。

Auth Router 决策（PRD §3.3）：
- `SAL_JAY_MONO`：AED → Jaywan
- `SAL_CO_BADGE`：AED → Jaywan / FX → MC MIP

数据来源：
- PRD 文档（PPC 项目下所有 PRD，包括 [[prd-review-salary-card-mono-cobadge-2026-05-13]]）
- 系统设计文档（卡平台、清结算、账务）
- 卡组织标准文档（Mastercard / Jaywan）

## QA 关注点

- **术语与流程对齐**：业务定义层是其他所有层的前提，术语和流程未对齐会导致规则、接口、用例偏差。Salary Card PRD 中 CAA / CPV / IHC / IPM / MIP / UAESWITCH / proxy_no / NARADA / SVF 等术语未定义，Glossary 缺失需补。
- **卡产品矩阵覆盖度**：Salary Card × Jaywan 行从 "TBD" 反哺为 ✅；发卡条件、币种、限额、目标用户、卡组织等差异需在 PRD freeze 后完整回填 KB `2134179950`。
- **卡生命周期状态机**：每个状态含义、合法转换、触发条件需明确。Salary Card 新卡 lifecycle 调 YSE APIs 时，CLOSED 卡是否会被授权 / NON_ZERO_BALANCE 关卡 / CLOSING 中再关卡的幂等需校验（关联 RL-018~020、EP-005、EP-007）。
- **账户模型映射**：卡 vs 钱包 vs 多币种子账户的对应关系。Co-badge 新 ledger 命名（jaywan pre-settlement / Jaywan Pending / MC Pending）与现有 KB §4 资金账户类型（Customer Basic / Customer Pending / Merchant Pending / Merchant Basic / Profit / Shortfall）不一致，需明确映射关系，否则会计入账规则会乱。
- **卡组织合规**：CBUAE 2026-03-31 AEP Mandate 为合规硬截止，涉及 Salary Card Mono + Co-badge 两个 program；Mastercard / Jaywan 标准文档对齐。
- **关键表与字段**：`t_card_bin` 新增 `product_code`、新 token_records 表（双 DPAN）需在 KB 三层补齐。
- **当前状态**为"骨架（待补充）"，主负责人 Jianfei Wang。PRD 落地后必须反哺的 KB 页：`2134179950` 卡产品矩阵、`2132803758` 卡组织规则差异、`2134966320` 限额体系、`2134835256` 卡组织接口、`2134179970` 关键表与字段、`2134835276` Zephyr 索引。

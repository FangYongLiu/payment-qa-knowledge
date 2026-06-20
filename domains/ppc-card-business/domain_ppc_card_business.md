---
id: domain_ppc_card_business
object_type: Domain
domain: ppc-card-business
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki_attachment
source_ref: wiki_attachment:e3c2c891-c5e7-47d3-9cfb-05825c9af14a
tags:
- prepaid-card
- jaywan
- mbank
- botim
- salary-card
subdomain: null
module: null
sensitivity: normal
name: PPC卡业务域
aliases: []
related_services: []
related_tables:
- t_card_bin
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述

PPC卡业务域属于业务定义层（创建于 2026-05-04，维护人：Jianfei Wang，状态：骨架待补充）。该层用途是让人和 AI "听懂" PPC 业务，是其他所有层的前提——如果术语和流程没对齐，后面的规则、接口、用例都会跑偏。

随 Salary Card Mono-badge & Co-badge PRD（2026-05-13 review）落地，本域卡产品矩阵从 "TBD" 转为已覆盖：新增 Salary Card × Jaywan Mono 与 Salary Card × MC×Jaywan Co-badge 两个 program，CBUAE Mandate 截止 2026-03-31。

新纳入扩展产品线 Jaywan Prepaid Card Integration with MBank（BRD v1.1）：以 MBank 为持牌 BIN Sponsor、Dgpays 为处理方，通过 Botim app 端到端发行与管理 Jaywan 虚拟卡与实体卡，支持实时余额同步、完整数字化生命周期与方案合规交易。

## 覆盖范围

本业务域覆盖 PPC 卡产品的端到端业务，包括：开卡、激活、消费授权、清算入账、退款、退单、销卡。

业务定义层应包含的内容：

- **卡产品矩阵**（KB id `2134179950`）：列出全部卡产品的差异（发卡条件、币种、限额、目标用户、卡组织）
  - Salary Card × Jaywan 行：原标 "待确认 TBD"，PRD 落地后改为 ✅，含 Mono + Co-badge 两个 program
  - Salary Card × Mastercard 行：✅（Co-badge 中 MC 分支）
  - 新增 Jaywan(MBank BIN Sponsor) 产品线：见 [[jaywan-product-matrix-and-setup]]
- **卡生命周期状态机**（KB id `2133393518`）：每个状态的含义、合法转换、触发条件
- **账户模型**：卡 vs 钱包 vs 多币种子账户 的对应关系
- **术语词典**：卡组织/支付/合规相关的所有术语（CAA / CPV / IHC / IPM / MIP / UAESWITCH / proxy_no / NARADA / SVF / BPS 等待补全）
- **业务主流程图**（KB id `2133196989`）：开卡、激活、消费授权、清算入账、退款、退单、销卡的端到端流程

Salary Card 新增 program 范围：

- **Salary Card Jaywan Mono**：PPC 托管，YSE 管理，EDC 印卡，Botim 用户端；仅支持 AED 国内交易，国际硬拒
- **Salary Card MC×Jaywan Co-badge**：Mastercard Prepaid Gold BIN + Jaywan onboard，AED 走 Jaywan / FX 走 MC
- 新 product code：`SALCOB`（Co-badge）/ `SALMOB`（Mono），plastic code `STDPLS*`
- `t_card_bin` 表新增 `product_code` 字段以区分双 scheme 路由

Jaywan(MBank) 集成范围（详见 [[jaywan-card-integration-scope]]）：
- Botim app 内虚拟卡与实体卡发卡、配送追踪
- Apple Pay / Google Pay 卡 tokenization
- PIN 创建与更新
- 卡完整生命周期：block、activate、replace、renew、closure
- 动态交易权限（ECOM / POS / ATM）
- MCC 交易限制
- 3DS 启用的电商支持
- 实时余额更新与查询
- 对账、退款、冲正与退单工作流

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

Auth Router 决策（Salary Card PRD §3.3）：
- `SAL_JAY_MONO`：AED → Jaywan
- `SAL_CO_BADGE`：AED → Jaywan / FX → MC MIP

Jaywan(MBank) 集成关键流程与制品：
- BRD 总览：[[jaywan-prepaid-card-brd-overview]]
- 集成功能范围：[[jaywan-card-integration-scope]]
- 门户与 MIS 报表：[[jaywan-portal-and-reporting]]
- 对账与结算（T+1，04:00 AM GST，SFTP，Excel/CSV，AED，CBUAE 通道）：[[jaywan-reconciliation-settlement]]
- 产品矩阵与产品设置（BIN/Program/Product Type/AED/PIN try=3/Random/Green/5Y/plastic/Fee/Limit）：[[jaywan-product-matrix-and-setup]]
- UAT、部署与依赖（BIN 启用、Dgpays pre-prod APIs、结算签字、快递就绪、SLA、产品建档）：[[jaywan-uat-deployment-dependencies]]

数据来源：
- PRD 文档（PPC 项目下所有 PRD，包括 [[prd-review-salary-card-mono-cobadge-2026-05-13]]）
- BRD 文档：Jaywan Prepaid Card Integration with MBank v1.1
- 系统设计文档（卡平台、清结算、账务）
- 卡组织标准文档（Mastercard / Jaywan）

## QA 关注点

- **术语与流程对齐**：业务定义层是其他所有层的前提，术语和流程未对齐会导致规则、接口、用例偏差。Salary Card PRD 中 CAA / CPV / IHC / IPM / MIP / UAESWITCH / proxy_no / NARADA / SVF 等术语未定义，Glossary 缺失需补。
- **卡产品矩阵覆盖度**：Salary Card × Jaywan 行从 "TBD" 反哺为 ✅；Jaywan(MBank) 虚拟/实体卡产品线需新增进矩阵；发卡条件、币种、限额、目标用户、卡组织等差异需在 PRD/BRD freeze 后完整回填 KB `2134179950`。
- **卡生命周期状态机**：每个状态含义、合法转换、触发条件需明确。Salary Card 新卡 lifecycle 调 YSE APIs 时，CLOSED 卡是

---
title: Salary Card Mono-badge & Co-badge 业务总览
domain: ppc-card-business
kind: wiki_page
slug: salary-card-mono-cobadge-overview
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2167636024
tags: []
related_services:
  - svc_cards
  - svc_ppc
related_tables:
  - tbl_ppc_t_virtual_card
---

# Salary Card Mono-badge & Co-badge 业务总览

> Salary Card 引入两个新 program——**Jaywan Mono-badge**（仅 AED 国内）与 **MC × Jaywan Co-badge**（AED 走 Jaywan / FX 走 Mastercard），用于满足 CBUAE 2026-03-31 AEP Mandate；目标 EOY 150K cards、Mono : Co-badge ≈ 80 : 20、节约 ~400K AED。

相关页：[[prd-review-salary-card-mono-cobadge-2026-05-13]] · [[salary-card-test-watch-points]] · [[domain_ppc_card_business]]

## 业务定义与产品边界

- **Mono-badge**：单一卡组织 = Jaywan；**仅支持 AED 国内交易，国际硬拒**。
- **Co-badge**：Mastercard Prepaid Gold BIN + Jaywan onboard；同一物理 PAN，AED 走 Jaywan、FX / 跨境走 MC MIP。
- 发卡链路：BPS（业务系统）→ PPC（托管）→ YSE（卡管理）→ EDC（印卡）→ Botim App（用户端）。
- 公司管理：Corporate Management 系统侧负责企业批量发卡。

## 费率与限额

| 项目 | Mono (Jaywan) | Co-badge (MC × Jaywan) |
|---|---|---|
| 发卡费 | 0~25 AED | — |
| 补卡费 | 26.25 AED | — |
| ATM 取现 | 2.05 AED | — |
| 余额查询 | 1.05 AED | — |
| 跨境/跨币种费 | n/a（硬拒国际） | **3.5%**（与 KB 现行 2.00% 冲突，待 PM 拍板） |
| ATM 单笔 | 3,000 AED | 3,000 AED |
| POS / Ecom 单笔 | 10,000 AED | 10,000 AED |
| 日 / 月限额 | "as per wallet specifications"（数值未明确） | 同左 |

> ⚠️ 多币种限额是否按 AED 等值合并、跨境费率最终值，均为 Open Question，详见 [[prd-review-salary-card-mono-cobadge-2026-05-13]]。

## 产品编码与 BIN 路由

- 新 product code：**SALCOB**（Co-badge）/ **SALMOB**（Mono）。
- 新 plastic code：**STDPLS***。
- `t_card_bin` 表区分双 scheme，按 `BIN + product_code` 路由。
- Card lifecycle CMS 调 YSE API 时按 BIN + product_code 决策；存 scheme 偏好。
- ⚠️ PRD 未给出灰度 / canary、误配检测、rollback 策略——这是 BIN 路由错配的最大风险点。

## 交易链路（Detailed Transaction Flows）

### 域内（UAE）五段式
`Customer → Acquirer → UAESWITCH → Jaywan → Botim/YSE → PPC`

- Jaywan **ECOM = dual-message**；POS / ATM = single-message。
- YSE PBAUTH 接口用 **proxy_no** 识别 scheme。

### 国际跨境
- Co-badge 卡 FX 交易归入 **Mastercard 既有 MIP 框架**。
- Mono 卡：**hard-fail 国际交易**（判定字段——currency / acquiring country / BIN——PRD 未明确）。

### Auth Router 决策
- `SAL_JAY_MONO`：AED → Jaywan。
- `SAL_CO_BADGE`：AED → Jaywan；FX → MC MIP。

## 清算 / 对账 / Ledger

- 新 ledger 三类账户：**jaywan pre-settlement / Jaywan Pending / MC Pending**。
  - ⚠️ 与 KB 限额体系 §4 现行命名（Customer Basic / Pending / Merchant Basic / Profit / Shortfall）不一致，需明确映射。
- Jaywan clearing 文件格式与 MC IPM 不同，需单独 ingest。
- 每日三方对账：scheme vs processor vs ledger。
- ⚠️ PRD 未覆盖：对账文件解析失败兜底、双 ledger Shortfall 归属、字段缺失/金额漂移处理。

## Tokenization

- 双 token service provider，同一物理 PAN 在设备钱包可能产生 **2 个 DPAN**（MC 一个 / Jaywan 一个）。
- 需存储字段：scheme、token_reference、lifecycle 状态。
- ⚠️ Open：PAN suspended/closed 时两 DPAN 是否联动 revoke、单边 token 创建失败的卡状态、scheme 单边 lifecycle 通知如何同步另一 scheme。

## 3DS

- **双 ACS**：Jaywan 与 MC 各一套 ACS 配置。
- 3DS 配置 per `product_code`。
- ⚠️ Open：双 scheme 的 challenge / frictionless 决策规则是否一致。

## UI / UX

- 卡 gallery 显示：
  - "Salary (Jaywan Mono) – UAE-only"
  - "Co-badge – UAE + International"

## 认证与环境

- 三环境：dev → UAT → pre-prod → prod。
- Jaywan UAT rails 经由 YSE。
- Mastercard 必过认证项：**CAA / CPV / IHC / Ecom / Tokenization**。
- ⚠️ 各认证项 timeline 与 owner 未列出，需对齐 CBUAE 2026-03-31 截止日。

## 上下游依赖

- **BPS**（业务系统） · **PPC**（托管） · **YSE**（卡管理 + Jaywan UAT rails） · **EDC**（印卡） · **Botim App**（用户端） · **Corporate Management**（企业批量）。
- ⚠️ 各依赖未列 owner / status / 关键路径。

## 监管合规

- **CBUAE 2026-03-31 AEP Mandate** 为硬截止——Salary Card Mono + Co-badge 两个 program 都受约束。

## Glossary（PRD 中出现但未定义）

CAA / CPV / IHC / IPM / MIP / UAESWITCH / proxy_no / NARADA / SVF / BPS / SALCOB / SALMOB / STDPLS*

## 核心风险速查

- **EP-019 BIN 路由错配** —— 缺灰度/检测/回滚（🔴）。
- **跨境费率 3.5% vs KB 2.00%** —— 需 PM 拍板（🔴）。
- **RL-001~008 多币种利润核算** —— Co-badge 跨境全套触发（🔴）。
- **RL-014~017 Auth-Clearing 不一致** —— Co-badge MIP 路径触发（🔴）。
- **RL-026 对账文件解析** —— Jaywan 新文件格式（🔴）。
- **双 Tokenization 单边失败** —— 卡半残风险（🟡）。

详细测试覆盖与回归矩阵见 [[salary-card-test-watch-points]]。

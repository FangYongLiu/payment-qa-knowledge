---
id: tbl_acquireii_t_dcc_info_log
object_type: Table
domain: device-pos
status: archived
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_dcc_info_log.md
tags:
- DCC
- 报价日志
- 汇率
subdomain: acquireii
module: dcc
sensitivity: normal
name: DCC信息日志表
aliases:
- t_dcc_info_log
- acquireii.t_dcc_info_log
related_services: []
related_tables:
- tbl_acquireii_t_acquire_order
- tbl_acquireii_t_card_info
- tbl_acquireii_t_dcc_info
- tbl_acquireii_t_payment_info
related_scenarios:
- scn_acquire_product_apply
- scn_merchant_transaction_db_check
related_logs: []
related_requirements: []
related_failures: []
---

## 表用途

`acquireii.t_dcc_info_log` 记录每一次 **DCC（Dynamic Currency Conversion，动态货币转换）报价请求**的详细日志，是 DCC 询价行为的明细流水。重要程度 ⭐⭐⭐。

每次商户/收银台向收单系统发起 DCC 询价，都会写入一条记录，包含：
- 报价时的金额（原币种 / DCC 币种）、汇率（含加点率 markup_rate）
- 报价对应的卡信息（card_token、card_ticket_id）
- 报价 ID（dcc_quote_id）和过期时间（dcc_expired），供后续支付时验证

### 与 `t_dcc_info` 的区别
| 表 | 维度 | 粒度 |
|---|---|---|
| `t_dcc_info` | 订单维度 | 一笔订单一条，记录最终采用的 DCC 信息 |
| `t_dcc_info_log` | 报价维度 | 一次询价一条，可能多次报价才产生一笔订单 |

二者通过 `partner_id + dcc_quote_id` 关联，关系为 **N:1**（多条报价日志对应一条最终 DCC 订单信息）。

## 在交易链路中的位置

```
商户/收银台询价  ──►  写 t_dcc_info_log（每次询价一条，含 quote_id + 过期时间）
        │
        ▼
用户选择 DCC 币种确认支付
        │
        ▼
收单下单（t_acquire_order）  ──►  写 t_dcc_info（订单维度，引用 quote_id）
        │
        ▼
支付指令（t_payment_info / t_command）按 DCC 金额扣款
```

卡信息（card_token / card_ticket_id）在询价阶段即落库，与 `t_card_info` 体系的脱敏 token 一致。

## 关键列

**主键 / 金额**
- `id` bigint：主键
- `order_amount` decimal(19,4) / `order_amount_cur` char(3)：原订单金额与币种
- `dcc_amount` decimal(19,4) / `dcc_amount_cur` char(3)：DCC 转换后金额与币种

**汇率 / 报价**
- `exchange_rate` decimal(16,8)：汇率
- `markup_rate` decimal(16,8)：加点率（DCC 收益率）
- `dcc_quote_id` varchar(64)：DCC 报价 ID（与外部 DCC 服务对齐）
- `dcc_expired` timestamp(3)：报价过期时间

**商户 / 卡**
- `partner_id` varchar(64)：商户 ID（必填）
- `card_ticket_id` varchar(64)：卡 UES ticket ID
- `card_token` varchar(64)：卡 Token（脱敏，非原 PAN）

**时间 / 版本**
- `created_time` / `last_updated_time` timestamp(3)
- `data_version` bigint

## 主键 / 索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | id | 主键 |
| `i_dil_ct` | created_time | 按时间范围查询 |
| `i_dil_pd` | (partner_id, dcc_quote_id) | 常用：按商户 + Quote ID 查报价历史 |

## 关联表

| 关联表 | 关系 | 关联字段 | 说明 |
|---|---|---|---|
| `t_dcc_info` | N:1 | `partner_id + dcc_quote_id` | 报价日志 → 订单维度 DCC 信息 |
| `t_acquire_order` | 间接 | 经 `t_dcc_info` 关联 | 最终采纳 DCC 报价的订单 |
| `t_payment_info` | 间接 | 经订单关联 | 实际扣款金额=DCC 金额 |
| `t_card_info` | 引用 | `card_token` / `card_ticket_id` | 询价对应的脱敏卡 |

## QA 落库检查要点

1. **报价过期检查**：使用 `dcc_quote_id` 前必须校验 `dcc_expired`，过期报价不可用于支付。可用 `dcc_expired < created_time` 排查异常报价。
2. **同一 quote 多次记录**：每次询价都会插入一条，按 `(partner_id, dcc_quote_id)` 查询可能返回多条，需按 `created_time DESC` 取最新。
3. **card_token 脱敏**：`card_token` / `card_ticket_id` 为脱敏标识，**不可当作 PAN 使用**，与 `t_card_info` 体系一致。
4. **金额币种成对**：`order_amount` 与 `order_amount_cur`、`dcc_amount` 与 `dcc_amount_cur` 必须配套；需校验 `dcc_amount ≈ order_amount × exchange_rate`（exchange_rate 已含 markup_rate）。
5. **必填字段**：`id`、`order_amount(_cur)`、`dcc_amount(_cur)`、`partner_id`、`created_time`、`last_updated_time`、`data_version` 不可为空。
6. **与 `t_dcc_info` 一致性**：当订单使用了某 quote_id，`t_dcc_info` 对应记录的金额、汇率应与本表中 `created_time DESC` 取到的最新一条 quote 一致。
7. **markup_rate 合理性**：通常应在配置区间内（>0 且小于业务上限），异常值需告警。

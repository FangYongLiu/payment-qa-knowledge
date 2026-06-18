---
id: tbl_acquireii_t_dcc_info_log
object_type: Table
domain: pos-business
status: active
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
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
记录每一次 DCC 报价请求的详细日志，包括：
- 报价时的金额、汇率（含加点率 markup_rate）
- 报价对应的卡信息（card_token、card_ticket_id）
- 报价过期时间（dcc_expired）
- 报价 ID（dcc_quote_id），用于后续支付时验证

与 `t_dcc_info` 的区别：
- `t_dcc_info`：订单维度，一笔订单一条
- `t_dcc_info_log`：报价维度，可能多次报价才产生一笔订单

表名：`acquireii.t_dcc_info_log`，重要程度 ⭐⭐⭐。

## 关键列
**主键/金额**
- `id` bigint：主键
- `order_amount` decimal(19,4) / `order_amount_cur` char(3)：原订单金额与币种
- `dcc_amount` decimal(19,4) / `dcc_amount_cur` char(3)：DCC 金额与币种

**汇率/报价**
- `exchange_rate` decimal(16,8)：汇率
- `markup_rate` decimal(16,8)：加点率
- `dcc_quote_id` varchar(64)：DCC 报价 ID
- `dcc_expired` timestamp(3)：报价过期时间

**商户/卡**
- `partner_id` varchar(64)：商户 ID（必填）
- `card_ticket_id` varchar(64)：卡 ues ticket ID
- `card_token` varchar(64)：卡 Token（脱敏，非原卡号）

**时间/版本**
- `created_time` / `last_updated_time` timestamp(3)
- `data_version` bigint

## 主键/索引
| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | id | 主键 |
| `i_dil_ct` | created_time | 按时间查 |
| `i_dil_pd` | (partner_id, dcc_quote_id) | 常用：按商户 + Quote ID 查报价历史 |

关联：`t_dcc_info` N:1，关联字段 `partner_id + dcc_quote_id`。

## 校验点(QA 关注)
1. **报价过期检查**：使用 `dcc_quote_id` 前必须校验 `dcc_expired`，过期不可用于支付。可用 `dcc_expired < created_time` 排查异常报价。
2. **同一 quote 多次记录**：每次询价都会插入一条，按 `(partner_id, dcc_quote_id)` 查询可能返回多条，需按 `created_time DESC` 取最新。
3. **card_token 脱敏**：日志中 `card_token`/`card_ticket_id` 非原卡号，不要当作 PAN 使用。
4. **金额币种成对**：`order_amount` 与 `order_amount_cur`、`dcc_amount` 与 `dcc_amount_cur` 必须配套，校验 DCC 金额 = 原金额 × exchange_rate（含 markup_rate）。
5. **必填字段**：`id`、`order_amount(_cur)`、`dcc_amount(_cur)`、`partner_id`、`created_time`、`last_updated_time`、`data_version` 不可为空。

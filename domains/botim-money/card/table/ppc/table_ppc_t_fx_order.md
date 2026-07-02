---
id: tbl_ppc_t_fx_order
object_type: Table
name: Foreign Exchange Order (t_fx_order)
aliases: [t_fx_order, ppc.t_fx_order]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ppc schema DDL
tags: [card, ppc]
sensitivity: normal
related_services: []
---

# Foreign Exchange Order (t_fx_order)

## 用途
物理表 `ppc.t_fx_order`,主键 `fx_voucher_no`。Foreign Exchange Order。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `fx_voucher_no` | bigint | Exchange Voucher Number |
| `request_no` | varchar(32) | Request Number |
| `virtual_card_id` | bigint | Virtual Card ID |
| `partner_id` | varchar(20) | Partner ID |
| `fx_order_type` | varchar(10) | Exchange Order Type: N=Normal, CC=Cancel Card |
| `source_amount` | decimal(19, 4) | Source Amount |
| `source_currency` | char(3) | Source Currency |
| `source_rate_version` | bigint | Source Rate Version · 可空 |
| `target_amount` | decimal(19, 4) | Target Amount |
| `target_currency` | char(3) | Target Currency |
| `target_rate_version` | bigint | Target Rate Version · 可空 |
| `fx_status` | char(2) | Exchange Status: P=Process, SW=Sync Wallet, S=Success, F=Fail |
| `payment_voucher_no` | bigint | Payment Voucher Number · 可空 |
| `trx_ref_no` | varchar(12) | Transaction Ref No · 可空 |
| `unity_result_code` | varchar(50) | Unity Result Code · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`fx_voucher_no`
- `idx_payment_order_no`:payment_voucher_no
- `idx_request_no`:request_no
- `idx_update_time_card_id`:update_time, virtual_card_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

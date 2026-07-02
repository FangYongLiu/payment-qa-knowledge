---
id: tbl_upic_t_upi_flow
object_type: Table
name: upi对账流水表 (t_upi_flow)
aliases: [t_upi_flow, upic.t_upi_flow]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: upic schema DDL
tags: [card, upic]
sensitivity: normal
related_services: []
---

# upi对账流水表 (t_upi_flow)

## 用途
物理表 `upic.t_upi_flow`,主键 `flow_voucher_no`。upi对账流水表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `flow_voucher_no` | bigint | 主键前八后九 |
| `upi_flow_id` | varchar(50) | 对账id |
| `trx_voucher_no` | bigint | 交易凭证 · 可空 |
| `orig_trx_voucher_no` | bigint | 原交易凭证 · 可空 |
| `transaction_type` | varchar(10) | 交易类型;DEBIT=借记，CREDIT=贷记 |
| `bill_amount` | decimal(19, 4) | 对账金额 |
| `bill_currency` | char(3) | 对账币种 |
| `flow_status` | varchar(32) | 流水状态;SUCCESS:流水发送成功；流水撤销:CANCEL；流水冲正：REVERSE；流水撤销冲正：CANCEL_REVERSE |
| `extension` | varchar(255) | 扩展备注信息 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`flow_voucher_no`
- `idx_create_time`:create_time
- `idx_trx_voucher_no`:trx_voucher_no
- `idx_upi_flow_id`:upi_flow_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_upic_t_dispute_notify_detail
object_type: Table
name: 差错退款明细 (t_dispute_notify_detail)
aliases: [t_dispute_notify_detail, upic.t_dispute_notify_detail]
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

# 差错退款明细 (t_dispute_notify_detail)

## 用途
物理表 `upic.t_dispute_notify_detail`,主键 `trx_voucher_no`。差错退款明细。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `trx_voucher_no` | bigint | 交易凭证 |
| `dispute_flow_id` | varchar(50) | dispute流水ID |
| `debit_flow_id` | varchar(50) | debit流水ID |
| `dispute_file_id` | int | 差错文件ID |
| `trx_amount` | decimal(19, 4) | 交易金额 |
| `trx_currency` | char(3) | 交易币种 |
| `bill_amount` | decimal(19, 4) | 计费金额 |
| `bill_currency` | char(3) | 计费币种 |
| `bill_conversion_rate` | decimal(19, 8) | Bill Conversion Rate |
| `dispute_detail_status` | char | 差错明细状态;P处理中 S成功 F失败 |
| `settle_amount` | decimal(19, 4) | 结算金额 |
| `settle_currency` | char(3) | 结算币种 |
| `sett_conv_rate` | decimal(19, 8) | Settle Conversion Rate |
| `sett_date` | timestamp | 结算日期 · 可空 |
| `conv_date` | varchar(10) | 汇率日期 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `extension` | varchar(255) | 扩展 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`trx_voucher_no`
- `idx_dispute_file_id`:dispute_file_id
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

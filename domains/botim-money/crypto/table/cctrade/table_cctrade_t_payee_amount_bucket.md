---
id: tbl_cctrade_t_payee_amount_bucket
object_type: Table
name: 收款方资金桶 (t_payee_amount_bucket)
aliases: [t_payee_amount_bucket, cctrade.t_payee_amount_bucket]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cctrade schema DDL
tags: [crypto, cctrade]
sensitivity: normal
related_services: []
---

# 收款方资金桶 (t_payee_amount_bucket)

## 用途
物理表 `cctrade.t_payee_amount_bucket`,主键 `id`。收款方资金桶。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 交易订单id |
| `trade_order_id` | bigint | 交易订单号 |
| `member_id` | varchar(32) | 会员ID |
| `refund_fee` | varchar(32) | 是否退费 |
| `stlb_pcpl_cny_code` | varchar(32) | 待结算本金币种 |
| `stlb_pcpl_pd_amount` | decimal(23, 8) | 待结算本金金额 |
| `stlb_fee_cny_code` | varchar(32) | 待结算费用币种 |
| `stlb_fee_pd_amount` | decimal(23, 8) | 待结算费用金额 |
| `balance_pd_cny_code` | varchar(32) | 余额预支币种 |
| `balance_pd_amount` | decimal(23, 8) | 余额预支金额 |
| `settling_cny_code` | varchar(32) | 结算中币种 |
| `settling_amount` | decimal(23, 8) | 结算中金额 |
| `stld_pcpl_cny_code` | varchar(32) | 已结算本金币种 |
| `stld_pcpl_amount` | decimal(23, 8) | 已结算本金金额 |
| `stld_fee_cny_code` | varchar(32) | 已结算费用币种 |
| `stld_fee_amount` | decimal(23, 8) | 已结算费用金额 |
| `refunding_stl_cny_code` | varchar(32) | 退结算中币种 |
| `refunding_stl_amount` | decimal(23, 8) | 退结算中金额 |
| `refunded_stl_cny_code` | varchar(32) | 已退结算金额 |
| `refunded_stl_amount` | decimal(23, 8) | 已退结算金额 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`id`
- `uk_pab_tmid`:trade_order_id, member_id (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

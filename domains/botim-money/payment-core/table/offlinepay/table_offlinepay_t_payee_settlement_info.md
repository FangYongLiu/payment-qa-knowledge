---
id: tbl_offlinepay_t_payee_settlement_info
object_type: Table
name: Payee Settlement Info (t_payee_settlement_info)
aliases: [t_payee_settlement_info, offlinepay.t_payee_settlement_info]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: offlinepay schema DDL
tags: [payment-core, offlinepay]
sensitivity: normal
related_services: []
---

# Payee Settlement Info (t_payee_settlement_info)

## 用途
物理表 `offlinepay.t_payee_settlement_info`,主键 `global_id`。Payee Settlement Info。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint | global_id |
| `fee_amount` | decimal(19, 4) | fee_amount · 可空 |
| `fee_amount_cur` | char(3) | fee_amount_currency · 可空 |
| `payee_amount` | decimal(19, 4) | payee_amount · 可空 |
| `payee_amount_cur` | char(3) | payee_amount_currency · 可空 |
| `created_time` | timestamp(3) | created_time |
| `last_updated_time` | timestamp(3) | last_updated_time |
| `data_version` | bigint | data_version |

## 主键 / 索引
- 主键:`global_id`
- `i_psi_ct`:created_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

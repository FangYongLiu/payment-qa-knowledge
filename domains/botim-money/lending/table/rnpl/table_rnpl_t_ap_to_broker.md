---
id: tbl_rnpl_t_ap_to_broker
object_type: Table
name: ap to broker (t_ap_to_broker)
aliases: [t_ap_to_broker, rnpl.t_ap_to_broker]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: rnpl schema DDL
tags: [lending, rnpl]
sensitivity: normal
related_services: []
---

# ap to broker (t_ap_to_broker)

## 用途
物理表 `rnpl.t_ap_to_broker`,主键 `id`。ap to broker。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `contract_id` | int | contract id |
| `cheque_no` | int | cheque no |
| `tprp_id` | int | tprp id |
| `due_time` | timestamp | duetime · 可空 |
| `amount` | decimal(15, 2) | amount |
| `currency` | char(3) | 待补 |
| `status` | tinyint | status |
| `pay_finish_time` | timestamp | pay finish time · 可空 |
| `create_time` | timestamp | 待补 |
| `update_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

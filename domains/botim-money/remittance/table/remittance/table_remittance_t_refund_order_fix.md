---
id: tbl_remittance_t_refund_order_fix
object_type: Table
name: refund order table fix (t_refund_order_fix)
aliases: [t_refund_order_fix, remittance.t_refund_order_fix]
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: remittance schema DDL
tags: [remittance, remittance]
sensitivity: normal
related_services: []
---

# refund order table fix (t_refund_order_fix)

## 用途
物理表 `remittance.t_refund_order_fix`,主键 `refund_order_no`。refund order table fix。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `refund_order_no` | bigint | refund order no |
| `order_no` | bigint | order no |
| `mid` | varchar(20) | member id · 可空 |
| `refund_amount` | decimal(19, 4) | refund amount |
| `currency` | char(3) | currency |
| `status` | char | status : P- processing,S- success,F- failed |
| `remark` | varchar(255) | remark · 可空 |
| `unity_result_code` | varchar(50) | unity result code · 可空 |
| `create_time` | timestamp | create time |
| `update_time` | timestamp | update time |

## 主键 / 索引
- 主键:`refund_order_no`
- `idx_order_no`:order_no
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

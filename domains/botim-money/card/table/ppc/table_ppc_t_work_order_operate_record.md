---
id: tbl_ppc_t_work_order_operate_record
object_type: Table
name: Work Order Operate Record (t_work_order_operate_record)
aliases: [t_work_order_operate_record, ppc.t_work_order_operate_record]
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

# Work Order Operate Record (t_work_order_operate_record)

## 用途
物理表 `ppc.t_work_order_operate_record`,主键 `record_id`。Work Order Operate Record。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `record_id` | bigint | Record ID |
| `work_order_id` | bigint | Work Order ID |
| `opt_type` | varchar(8) | Operate Type: US=Update Status |
| `orig_value` | varchar(255) | Original Value |
| `new_value` | varchar(255) | New Value |
| `operator` | varchar(50) | Operator |
| `memo` | varchar(100) | Memo · 可空 |
| `create_time` | timestamp | Create time |

## 主键 / 索引
- 主键:`record_id`
- `idx_create_time`:create_time
- `idx_work_order_id`:work_order_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

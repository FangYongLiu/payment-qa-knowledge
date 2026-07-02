---
id: tbl_invoice_t_invoice_task
object_type: Table
name: es同步任务 (t_invoice_task)
aliases: [t_invoice_task, invoice.t_invoice_task]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: invoice schema DDL
tags: [merchant-management, invoice]
sensitivity: normal
related_services: []
---

# es同步任务 (t_invoice_task)

## 用途
物理表 `invoice.t_invoice_task`,主键 `id`。es同步任务。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `task_type` | varchar(32) | 任务类型 |
| `object_type` | varchar(32) | 对象类型 |
| `object_id` | varchar(32) | 对象id |
| `status` | varchar(32) | 状态 |
| `fail_code` | varchar(50) | 错误码 · 可空 |
| `fail_message` | varchar(200) | 错误描述 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`id`
- `i_task_lut`:last_updated_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

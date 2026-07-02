---
id: tbl_basis_t_operation_user_record
object_type: Table
name: 运营用户会话记录表 (t_operation_user_record)
aliases: [t_operation_user_record, basis.t_operation_user_record]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: basis schema DDL
tags: [merchant-management, basis]
sensitivity: normal
related_services: []
---

# 运营用户会话记录表 (t_operation_user_record)

## 用途
物理表 `basis.t_operation_user_record`,主键 `id`。运营用户会话记录表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 会话ID：前八后九 |
| `phone_number` | varchar(64) | 用户手机号 · 可空 |
| `operator` | varchar(64) | 操作员 · 可空 |
| `service_time` | timestamp | 服务时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

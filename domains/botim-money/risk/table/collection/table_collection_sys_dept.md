---
id: tbl_collection_sys_dept
object_type: Table
name: 部门 (sys_dept)
aliases: [sys_dept, collection.sys_dept]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: collection schema DDL
tags: [risk, collection]
sensitivity: normal
related_services: []
---

# 部门 (sys_dept)

## 用途
物理表 `collection.sys_dept`,主键 `dept_id`。部门。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `dept_id` | bigint | ID · 可空 |
| `pid` | bigint | 上级部门 · 可空 |
| `sub_count` | int(5) | 子部门数目 · 可空 |
| `name` | varchar(255) | 名称 |
| `dept_sort` | int(5) | 排序 · 可空 |
| `enabled` | tinyint(5) | 状态 |
| `create_by` | varchar(100) | 创建者 · 可空 |
| `update_by` | varchar(100) | 更新者 · 可空 |
| `create_time` | timestamp | 创建日期 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`dept_id`
- `inx_enabled`:enabled
- `inx_pid`:pid

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

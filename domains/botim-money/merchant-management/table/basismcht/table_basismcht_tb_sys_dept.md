---
id: tbl_basismcht_tb_sys_dept
object_type: Table
name: 部门表 (tb_sys_dept)
aliases: [tb_sys_dept, basismcht.tb_sys_dept]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: basismcht schema DDL
tags: [merchant-management, basismcht]
sensitivity: normal
related_services: []
---

# 部门表 (tb_sys_dept)

## 用途
物理表 `basismcht.tb_sys_dept`,主键 `dept_id`。部门表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `dept_id` | bigint | 主键id |
| `pid` | bigint | 父部门id · 可空 |
| `pids` | varchar(512) | 父级ids · 可空 |
| `simple_name` | varchar(45) | 简称 · 可空 |
| `full_name` | varchar(255) | 全称 · 可空 |
| `description` | varchar(255) | 描述 · 可空 |
| `version` | int | 版本（乐观锁保留字段） · 可空 |
| `sort` | int | 排序 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 修改时间 · 可空 |
| `create_user` | bigint | 创建人 · 可空 |
| `update_user` | bigint | 修改人 · 可空 |

## 主键 / 索引
- 主键:`dept_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

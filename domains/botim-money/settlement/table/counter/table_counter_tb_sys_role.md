---
id: tbl_counter_tb_sys_role
object_type: Table
name: 角色表 (tb_sys_role)
aliases: [tb_sys_role, counter.tb_sys_role]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: counter schema DDL
tags: [settlement, counter]
sensitivity: normal
related_services: []
---

# 角色表 (tb_sys_role)

## 用途
物理表 `counter.tb_sys_role`,主键 `role_id`。角色表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `role_id` | bigint | 主键id |
| `pid` | bigint | 父角色id · 可空 |
| `name` | varchar(255) | 角色名称 · 可空 |
| `description` | varchar(255) | 提示 · 可空 |
| `sort` | int | 序号 · 可空 |
| `version` | int | 乐观锁 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 修改时间 · 可空 |
| `create_user` | bigint | 创建用户 · 可空 |
| `update_user` | bigint | 修改用户 · 可空 |

## 主键 / 索引
- 主键:`role_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

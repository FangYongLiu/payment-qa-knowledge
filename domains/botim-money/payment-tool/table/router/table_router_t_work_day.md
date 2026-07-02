---
id: tbl_router_t_work_day
object_type: Table
name: 工作日表 (t_work_day)
aliases: [t_work_day, router.t_work_day]
domain: payment-tool
status: active
owner: kingo.liang
reviewer: kingo.liang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: router schema DDL
tags: [payment-tool, router]
sensitivity: normal
related_services: []
---

# 工作日表 (t_work_day)

## 用途
物理表 `router.t_work_day`,主键 `date_str, workday_group`。工作日表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `date_str` | varchar(8) | 日期格式 |
| `workday_group` | varchar(3) | 分组, F |
| `is_workday` | char | 是否为工作日, Y-是 N-否 · 可空 |
| `memo` | varchar(64) | 备注 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`date_str, workday_group`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

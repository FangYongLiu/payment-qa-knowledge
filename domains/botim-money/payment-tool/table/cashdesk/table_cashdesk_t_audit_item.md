---
id: tbl_cashdesk_t_audit_item
object_type: Table
name: 审核项 (t_audit_item)
aliases: [t_audit_item, cashdesk.t_audit_item]
domain: payment-tool
status: active
owner: kingo.liang
reviewer: kingo.liang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cashdesk schema DDL
tags: [payment-tool, cashdesk]
sensitivity: normal
related_services: []
---

# 审核项 (t_audit_item)

## 用途
物理表 `cashdesk.t_audit_item`,主键 `id`。审核项。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键 · 可空 |
| `audit_id` | bigint(18) | 审核id |
| `origin_data_id` | bigint(18) | 原数据id · 可空 |
| `origin_data_json` | varchar(500) | 原数据（JSON） · 可空 |
| `data_del_flag` | char | 数据删除标记（Y：删除 N:不删除）默认：N · 可空 |
| `data_json` | varchar(500) | 新数据（JSON） · 可空 |
| `gmt_created` | timestamp | 创建时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idex_audit_id`:audit_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

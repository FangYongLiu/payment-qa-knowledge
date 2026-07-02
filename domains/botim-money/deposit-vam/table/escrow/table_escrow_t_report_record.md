---
id: tbl_escrow_t_report_record
object_type: Table
name: 虚拟卡报表 (t_report_record)
aliases: [t_report_record, escrow.t_report_record]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: escrow schema DDL
tags: [deposit-vam, escrow]
sensitivity: normal
related_services: []
---

# 虚拟卡报表 (t_report_record)

## 用途
物理表 `escrow.t_report_record`,主键 `report_record_id`。虚拟卡报表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `report_record_id` | int | 主键 · 可空 |
| `record_name` | varchar(64) | 记录名 · 可空 |
| `gmt_start` | timestamp | 起始日期 · 可空 |
| `gmt_end` | timestamp | 截止时间 · 可空 |
| `status` | char | 状态 · 可空 |
| `memo` | varchar(128) | 备注 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`report_record_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_escrow_t_report_schedule
object_type: Table
name: 报备时间表 (t_report_schedule)
aliases: [t_report_schedule, escrow.t_report_schedule]
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

# 报备时间表 (t_report_schedule)

## 用途
物理表 `escrow.t_report_schedule`,主键 `id`。报备时间表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(19) | id · 可空 |
| `report_type` | varchar(4) | 报备类型。C-CREDIT；D-DEBIT；B-BALANCE；H-CARD_HOLDERS |
| `concurrent_tag` | varchar(32) | concurrentTag · 可空 |
| `status` | varchar(4) | task生成状态，F-FAIL失败，S-Success成功 |
| `next_exec_time` | timestamp | 下一次处理的时间 · 可空 |
| `last_exec_time` | timestamp | 上一次处理的时间 · 可空 |
| `skip_type` | varchar(32) | 跳过规则类型 |
| `skip_rule` | varchar(255) | 跳过的规则 |
| `start_rule` | varchar(255) | 开始的规则 |
| `end_rule` | varchar(255) | 结束规则 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modify` | timestamp | 更新时间 · 可空 |
| `weight` | tinyint | task权重 |
| `next_trigger_cron` | varchar(32) | 下一个执行时间的触发corn · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

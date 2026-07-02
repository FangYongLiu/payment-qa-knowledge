---
id: tbl_escrow_t_report_task
object_type: Table
name: 文件上报task表 (t_report_task)
aliases: [t_report_task, escrow.t_report_task]
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

# 文件上报task表 (t_report_task)

## 用途
物理表 `escrow.t_report_task`,主键 `id`。文件上报task表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(19) | id |
| `file_name` | varchar(255) | 文件名 · 可空 |
| `report_type` | varchar(4) | 报备类型。C-CREDIT；D-DEBIT；B-BALANCE；H-CARD_HOLDERS |
| `start_time` | timestamp | 起始时间 · 可空 |
| `end_time` | timestamp | 结束时间 · 可空 |
| `status` | varchar(4) | 上报task执行状态，I-INIT初始化，P-PROCESS处理中,F-FAIL上报失败,R-RETRY待重试,S-SUCCESS上报成功 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modify` | timestamp | 更新时间 · 可空 |
| `weight` | tinyint | task权重 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

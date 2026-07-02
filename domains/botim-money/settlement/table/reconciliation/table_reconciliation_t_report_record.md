---
id: tbl_reconciliation_t_report_record
object_type: Table
name: 资金对账报表记录 (t_report_record)
aliases: [t_report_record, reconciliation.t_report_record]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: reconciliation schema DDL
tags: [settlement, reconciliation]
sensitivity: normal
related_services: []
---

# 资金对账报表记录 (t_report_record)

## 用途
物理表 `reconciliation.t_report_record`,主键 `flow_id`。资金对账报表记录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `flow_id` | bigint(17) | 主键 |
| `report_type` | varchar(8) | 报表类型 · 可空 |
| `start_date` | date | 起始日期 · 可空 |
| `end_date` | date | 截止日期 · 可空 |
| `status` | varchar(8) | 报表生成状态 · 可空 |
| `message` | varchar(255) | 报表生成信息 · 可空 |
| `operator` | varchar(64) | 操作者 · 可空 |
| `memo` | varchar(255) | 备注信息 · 可空 |
| `file_name` | varchar(255) | 报表名称(ufs ossPah) · 可空 |
| `oss_path` | varchar(255) | OssPath · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |
| `channel_list` | varchar(1024) | 渠道列表信息 多个渠道时以逗号,隔开 · 可空 |

## 主键 / 索引
- 主键:`flow_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

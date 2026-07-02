---
id: tbl_escrow_t_data_report
object_type: Table
name: 报备记录表 (t_data_report)
aliases: [t_data_report, escrow.t_data_report]
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

# 报备记录表 (t_data_report)

## 用途
物理表 `escrow.t_data_report`,主键 `id`。报备记录表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(19) | id |
| `file_name` | varchar(255) | 文件名 |
| `report_type` | varchar(4) | 报备类型。C-CREDIT；D-DEBIT；B-BALANCE；H-CARD_HOLDERS |
| `file_tag` | varchar(255) | 文件tag · 可空 |
| `report_time` | timestamp | 上报时间 |
| `batch_no` | varchar(64) | 批次编号 |
| `total_amount` | decimal(19, 4) | 总金额 · 可空 |
| `count` | int(10) | 上报数量 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modify` | timestamp | 更新时间 · 可空 |
| `status` | varchar(4) | 上报状态，F-ForReport待上报，R-Reported已上报，D-Dismissed已驳回 |
| `task_id` | varchar(64) | task编号 |
| `currency` | varchar(8) | 币种 · 可空 |
| `memo` | varchar(512) | memo · 可空 |
| `check_status` | varchar(4) | 校验状态,S-成功,F-失败 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

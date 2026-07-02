---
id: tbl_escrow_t_report_rule
object_type: Table
name: t_report_rule (t_report_rule)
aliases: [t_report_rule, escrow.t_report_rule]
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

# t_report_rule (t_report_rule)

## 用途
物理表 `escrow.t_report_rule`,主键 `report_rule_id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `report_rule_id` | int | 报告规则id · 可空 |
| `direction` | varchar(32) | 余额变动方向,positive-正向,negtive-反向 |
| `biz_product_code` | varchar(255) | 业务产品码,逗号分割 |
| `clearing_code` | varchar(64) | 清算编码,逗号分割 · 可空 |
| `sub_clearing_code` | varchar(32) | Sub Clearing Code, split by comma · 可空 |
| `report_category` | varchar(32) | 类型分类 |
| `memo` | varchar(128) | 备注 · 可空 |
| `report_remark` | varchar(128) | 报告备注 · 可空 |
| `is_default` | varchar(1) | 默认值 · 可空 |
| `orders` | int | 规则排序 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`report_rule_id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

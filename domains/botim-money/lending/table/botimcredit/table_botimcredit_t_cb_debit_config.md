---
id: tbl_botimcredit_t_cb_debit_config
object_type: Table
name: autodebit (t_cb_debit_config)
aliases: [t_cb_debit_config, botimcredit.t_cb_debit_config]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: botimcredit schema DDL
tags: [lending, botimcredit]
sensitivity: normal
related_services: []
---

# autodebit (t_cb_debit_config)

## 用途
物理表 `botimcredit.t_cb_debit_config`,主键 `id`。autodebit。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | primary key · 可空 |
| `status` | varchar(20) | 待补 |
| `product_code` | varchar(20) | product code · 可空 |
| `start` | varchar(20) | start · 可空 |
| `end` | varchar(20) | end · 可空 |
| `time` | varchar(20) | time · 可空 |
| `percentage` | varchar(20) | percentage · 可空 |
| `success_context` | varchar(200) | success context · 可空 |
| `fail_context` | varchar(200) | fail context · 可空 |
| `partner_id` | varchar(20) | partner id · 可空 |
| `ext` | varchar(255) | ext · 可空 |
| `create_time` | timestamp | 待补 |
| `update_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

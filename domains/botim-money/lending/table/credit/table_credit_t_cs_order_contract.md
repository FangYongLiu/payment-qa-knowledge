---
id: tbl_credit_t_cs_order_contract
object_type: Table
name: t_cs_order_contract (t_cs_order_contract)
aliases: [t_cs_order_contract, credit.t_cs_order_contract]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: credit schema DDL
tags: [lending, credit]
sensitivity: normal
related_services: []
---

# t_cs_order_contract (t_cs_order_contract)

## 用途
物理表 `credit.t_cs_order_contract`,主键 `id`。t_cs_order_contract。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(10) | 待补 · 可空 |
| `user_id` | varchar(32) | 待补 |
| `order_no` | varchar(64) | 待补 |
| `signed` | tinyint | 1:yes 0:no |
| `signed_method` | tinyint | 1:opt 2:face 3:other |
| `signed_time` | timestamp | 待补 |
| `contract_type` | varchar(32) | 待补 |
| `file_tag` | varchar(128) | 待补 · 可空 |
| `created_time` | timestamp | 待补 |
| `last_modified` | timestamp | 待补 |
| `flag` | tinyint | 0：历史 1：当前 |

## 主键 / 索引
- 主键:`id`
- `idx_order_no`:order_no
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

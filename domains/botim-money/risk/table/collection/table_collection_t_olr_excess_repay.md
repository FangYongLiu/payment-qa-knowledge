---
id: tbl_collection_t_olr_excess_repay
object_type: Table
name: 溢缴款表 (t_olr_excess_repay)
aliases: [t_olr_excess_repay, collection.t_olr_excess_repay]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: collection schema DDL
tags: [risk, collection]
sensitivity: normal
related_services: []
---

# 溢缴款表 (t_olr_excess_repay)

## 用途
物理表 `collection.t_olr_excess_repay`,主键 `id`。溢缴款表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(10) | 主健 · 可空 |
| `create_by` | varchar(50) | 创建者 · 可空 |
| `update_by` | varchar(50) | 更新人员 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |
| `uid` | varchar(50) | uuid |
| `member_id` | varchar(20) | 用户id |
| `audit_id` | varchar(50) | 审核id |
| `reference` | varchar(150) | reference |
| `repay_date` | date | 还款时间 |
| `repay_amount` | decimal(10, 2) | 还款金额 |
| `excess_amount` | decimal(10, 2) | 溢出金额 |
| `product` | tinyint(5) | 产品码 |
| `status` | tinyint(5) | 状态初始0 处理1 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_audit_id`:audit_id
- `idx_member_id`:member_id
- `idx_reference`:reference

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

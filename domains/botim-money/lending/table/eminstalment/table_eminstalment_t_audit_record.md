---
id: tbl_eminstalment_t_audit_record
object_type: Table
name: 风控审核记录表 (t_audit_record)
aliases: [t_audit_record, eminstalment.t_audit_record]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: eminstalment schema DDL
tags: [lending, eminstalment]
sensitivity: normal
related_services: []
---

# 风控审核记录表 (t_audit_record)

## 用途
物理表 `eminstalment.t_audit_record`,主键 `id`。风控审核记录表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | id · 可空 |
| `application_id` | varchar(64) | 传入到风控系统（anubis）的applicationId |
| `credit_order_id` | int | 对应credit_order表的id字段 |
| `status` | smallint(4) | 状态：0：初始状态，1：审核中，2：审核完毕 |
| `create_time` | timestamp | 待补 |
| `update_time` | timestamp | 待补 |
| `suggestion` | smallint(4) | 1:审核通过，0：审核拒绝 · 可空 |
| `reason_code` | smallint(4) | 待补 · 可空 |
| `amount` | decimal(10, 2) | 批准的额度 · 可空 |
| `aprvd_product_ids` | varchar(16) | 批准使用的分期产品id（对应t_product表的id）列表，用英文逗号分隔 · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_an`:application_id (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

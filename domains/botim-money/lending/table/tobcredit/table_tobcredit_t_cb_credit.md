---
id: tbl_tobcredit_t_cb_credit
object_type: Table
name: 授信表 (t_cb_credit)
aliases: [t_cb_credit, tobcredit.t_cb_credit]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: tobcredit schema DDL
tags: [lending, tobcredit]
sensitivity: normal
related_services: []
---

# 授信表 (t_cb_credit)

## 用途
物理表 `tobcredit.t_cb_credit`,主键 `id`。授信表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 启用标识 · 可空 |
| `uid` | varchar(64) | 授信唯一ID · 可空 |
| `status` | varchar(10) | 状态 · 可空 |
| `amount` | decimal(19, 4) | 授信金额 · 可空 |
| `partner_id` | varchar(20) | 商户ID · 可空 |
| `source` | varchar(10) | 授信来源 · 可空 |
| `memo` | varchar(512) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_partner_id`:partner_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

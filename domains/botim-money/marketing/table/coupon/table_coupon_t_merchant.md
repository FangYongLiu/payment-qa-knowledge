---
id: tbl_coupon_t_merchant
object_type: Table
name: 商户表 (t_merchant)
aliases: [t_merchant, coupon.t_merchant]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: coupon schema DDL
tags: [marketing, coupon]
sensitivity: normal
related_services: []
---

# 商户表 (t_merchant)

## 用途
物理表 `coupon.t_merchant`,主键 `merchant_id`。商户表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `merchant_id` | bigint | 主键 |
| `merchant_name` | varchar(32) | 商户名称 |
| `desc` | text | 商家介绍 · 可空 |
| `logo` | varchar(255) | 商户logo |
| `pin_code` | varchar(32) | 商户pin码 · 可空 |
| `status` | varchar(32) | 状态 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`merchant_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

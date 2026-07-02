---
id: tbl_coupon_t_package_price
object_type: Table
name: 套餐价格配置 (t_package_price)
aliases: [t_package_price, coupon.t_package_price]
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

# 套餐价格配置 (t_package_price)

## 用途
物理表 `coupon.t_package_price`,主键 `id`。套餐价格配置。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 |
| `package_id` | varchar(16) | 商品id · 可空 |
| `face_value` | decimal(15, 4) | 面值 · 可空 |
| `original_price` | decimal(19, 4) | 原价 · 可空 |
| `prevailing_price` | decimal(19, 4) | 现价 · 可空 |
| `currency` | varchar(3) | 币种 · 可空 |
| `status` | varchar(3) | 状态（1：上架 0：下架） |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 修改时间 |
| `extension` | varchar(255) | 额外信息 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_coupon_t_coupon_category
object_type: Table
name: 优惠券分类 (t_coupon_category)
aliases: [t_coupon_category, coupon.t_coupon_category]
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

# 优惠券分类 (t_coupon_category)

## 用途
物理表 `coupon.t_coupon_category`,主键 `category_id`。优惠券分类。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `category_id` | bigint | 分类id |
| `parent_id` | bigint | 父类id · 可空 |
| `category_name` | varchar(32) | 分类名称 |
| `index` | int | 排序 · 可空 |
| `status` | varchar(12) | 状态 |
| `show_flag` | varchar(12) | 是否展示 |
| `category_source` | varchar(12) | OMC:合作商户；OMC:外部商户 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`category_id`
- `idx_created_time`:created_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

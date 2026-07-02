---
id: tbl_coupon_t_coupon_usage_limit
object_type: Table
name: t_coupon_usage_limit (t_coupon_usage_limit)
aliases: [t_coupon_usage_limit, coupon.t_coupon_usage_limit]
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

# t_coupon_usage_limit (t_coupon_usage_limit)

## 用途
物理表 `coupon.t_coupon_usage_limit`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 |
| `data_type` | varchar(12) | RULE表示走dataeden；DEFAULT表示默认一般比较值 · 可空 |
| `data_key` | varchar(12) | 待补 · 可空 |
| `compare_val` | varchar(255) | 对比值 · 可空 |
| `c_type` | varchar(12) | INNER内部使用 CONFIG页面配置使用 · 可空 |
| `status` | tinyint | 是否可用 0 不可用 1可用 · 可空 |
| `coupon_id` | bigint | 优惠券id · 可空 |
| `op_type` | varchar(12) | 操作符（eq，lt，le，gt，ge，in） · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- `idx_coupon_id`:coupon_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

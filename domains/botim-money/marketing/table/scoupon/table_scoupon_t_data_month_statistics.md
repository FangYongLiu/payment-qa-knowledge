---
id: tbl_scoupon_t_data_month_statistics
object_type: Table
name: 券月统计表 (t_data_month_statistics)
aliases: [t_data_month_statistics, scoupon.t_data_month_statistics]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: scoupon schema DDL
tags: [marketing, scoupon]
sensitivity: normal
related_services: []
---

# 券月统计表 (t_data_month_statistics)

## 用途
物理表 `scoupon.t_data_month_statistics`,主键 `id`。券月统计表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键id |
| `member_id` | varchar(32) | 用户id |
| `total_face_value` | decimal(19, 4) | 券总面额 |
| `total_discount_price` | decimal(19, 4) | 券总优惠价格 |
| `currency` | char(3) | 币种 |
| `total_chances` | int | 总机会次数 |
| `total_used_chances` | int | 总已使用次数 |
| `month` | int | 月份 |

## 主键 / 索引
- 主键:`id`
- `idx_member_id`:member_id

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

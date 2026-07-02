---
id: tbl_coupon_t_stock_adjust_log
object_type: Table
name: t_stock_adjust_log (t_stock_adjust_log)
aliases: [t_stock_adjust_log, coupon.t_stock_adjust_log]
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

# t_stock_adjust_log (t_stock_adjust_log)

## 用途
物理表 `coupon.t_stock_adjust_log`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(12) | 主键 · 可空 |
| `campaign_id` | bigint | 活动id · 可空 |
| `coupon_id` | bigint | 优惠券id |
| `old_stock` | int(12) | 老库存值 · 可空 |
| `new_stock` | int(12) | 新库存值 · 可空 |
| `op_user` | varchar(64) | 操作人 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

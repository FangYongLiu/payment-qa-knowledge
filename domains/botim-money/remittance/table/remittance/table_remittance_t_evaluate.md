---
id: tbl_remittance_t_evaluate
object_type: Table
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (remittance schema) 2026-06-25
tags:
- remittance
- remittance
- t_evaluate
subdomain: remittance
module: null
sensitivity: normal
name: 评级(t_evaluate)
aliases:
- t_evaluate
related_services:
- svc_remittance
related_scenarios: []
---
# 评级(t_evaluate)

## 用途
评级。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键;8+9 |
| `order_no` | bigint | NOT NULL | 订单号;如remittance订单号 |
| `rating_level` | varchar(7) | NOT NULL | 评级等级 |
| `rating_score` | varchar(7) | NOT NULL | 评级分数 |
| `opinion_items` | varchar(255) |  | 评级内容;用竖杠|分割 |
| `feed_back` | varchar(500) |  | 用户反馈 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_order_no` (order_no)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

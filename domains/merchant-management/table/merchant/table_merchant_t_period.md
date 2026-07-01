---
id: tbl_merchant_t_period
object_type: Table
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (merchant schema) 2026-06-25
tags:
- merchant
- merchant
- t_period
subdomain: merchant
module: null
sensitivity: normal
name: 账期(t_period)
aliases:
- t_period
related_services:
- svc_merchant
related_scenarios: []
---
# 账期(t_period)

## 用途
账期。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | group id |
| `begin_date` | timestamp | NOT NULL | 开始日期 |
| `end_date` | timestamp | NOT NULL | 结束日期 |
| `period_type` | varchar(20) | NOT NULL | 期限类型 DAILY 日； MONTHLY 月 |
| `total_order_nums` | int | NOT NULL | 总订单数 |
| `completed_order_nums` | int | NOT NULL | 已完成订单数 |
| `status` | varchar(50) | NOT NULL | 状态 CREATED 已创建;  STARTED 已开始；DISPATCHED 已匹配；FINISHED 已完成 |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `last_updated_time` | timestamp | NOT NULL | 最后更新时间 |
| `data_version` | bigint | NOT NULL | 数据版本 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

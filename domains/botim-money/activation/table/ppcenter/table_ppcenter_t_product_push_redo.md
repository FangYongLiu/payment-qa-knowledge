---
id: tbl_ppcenter_t_product_push_redo
object_type: Table
domain: activation
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (ppcenter schema) 2026-06-25
tags:
- ppcenter
- pricing
- t_product_push_redo
subdomain: pricing
module: null
sensitivity: normal
name: 产品推送重做(t_product_push_redo)
aliases:
- t_product_push_redo
related_services:
- svc_ppcenter
related_scenarios: []
---
# 产品推送重做(t_product_push_redo)

## 用途
产品推送重做。属 ppcenter 库,由 [[svc_ppcenter]] 读写。

## 关联关系
- **所属服务**:[[svc_ppcenter]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | 主键 |
| `apply_id` | int | NOT NULL | 申请id |
| `status` | tinyint(2) | NOT NULL | 0:初始化；1:重试中；2重试失败；3重试成功 |
| `max_retry_times` | int(5) | NOT NULL | 最大重试次数 |
| `retried_times` | int(5) | NOT NULL | 重试次数 |
| `retry_memo` | varchar(255) |  | 重试备注 |
| `gmt_create` | timestamp | NOT NULL | 创建时间 |
| `gmt_modified` | timestamp | 默认 CURRENT_TIMESTAMP | 修改时间 |
| `gmt_next_notify` | timestamp |  | 下次重试时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

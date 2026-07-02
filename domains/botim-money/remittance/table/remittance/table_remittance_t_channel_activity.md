---
id: tbl_remittance_t_channel_activity
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
- t_channel_activity
subdomain: remittance
module: null
sensitivity: normal
name: t_channel_activity
aliases:
- t_channel_activity
related_services:
- svc_remittance
related_scenarios: []
---
# t_channel_activity

## 用途
待补。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | 主键 |
| `from_amount` | decimal(19,4) |  | 汇款金额 |
| `to_amount` | decimal(19,4) |  | 到账金额 |
| `to_country_code` | char(2) |  | 到账国家code |
| `to_currency` | char(3) |  | 到账币种 |
| `activity_name` | varchar(255) |  | 活动名称 |
| `activity_title` | varchar(255) |  | 活动标题 |
| `activity_sub_title` | varchar(255) |  | 活动子标题 |
| `content` | text |  | 活动内容 |
| `activity_footer` | varchar(255) |  | 活动页脚 |
| `img_link` | varchar(64) |  | 图片链接地址 |
| `status` | char | NOT NULL | Y：有效；N：无效 |
| `start_time` | timestamp | NOT NULL | 开始时间 |
| `end_time` | timestamp | NOT NULL | 结束时间 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 修改时间 |
| `lang_type` | char(3) |  | Lnag Type |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_activity_create_time` (create_time)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

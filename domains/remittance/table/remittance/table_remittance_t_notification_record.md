---
id: tbl_remittance_t_notification_record
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
- t_notification_record
subdomain: remittance
module: null
sensitivity: normal
name: 通知记录(t_notification_record)
aliases:
- t_notification_record
related_services:
- svc_remittance
related_scenarios: []
---
# 通知记录(t_notification_record)

## 用途
通知记录。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `record_id` | bigint | PK / NOT NULL | 主键 |
| `event_id` | bigint | NOT NULL | 配置id |
| `order_no` | bigint | NOT NULL | 订单号 |
| `notice_method` | varchar(7) | NOT NULL | 通知方式(MAIL-邮件,SMS-短信,NOA-公众号) |
| `notice_party` | varchar(8) | NOT NULL | payer，payee，platform |
| `member_id` | varchar(20) |  | 会员号 |
| `target_address` | varchar(32) | NOT NULL | 通知目标 |
| `partner_id` | varchar(20) | NOT NULL | 通知平台方id |
| `next_time` | timestamp | NOT NULL | 下次通知时间 |
| `template_id` | varchar(64) | NOT NULL | SMS和MAIL配置mns模板ID，NOA配置placeholder |
| `subject` | varchar(100) |  | 主题 |
| `notice_content` | varchar(2000) |  | notice content |
| `icon` | varchar(64) |  | icon |
| `retry_times` | int |  | 已重试次数 |
| `max_retry_times` | int |  | 最大重试次数 |
| `retry_rule` | varchar(64) |  | 重试规则 |
| `status` | char(2) | NOT NULL | 状态(P - 待通知,S - 通知成功,F - 失败,E - 异常) |
| `params` | varchar(255) |  | 通知变量 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`record_id`)
- 索引:
  - `idx_not_rec_eve_id` (event_id)
  - `idx_not_rec_ord_no` (order_no)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

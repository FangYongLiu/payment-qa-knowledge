---
id: tbl_remittance_t_notification_config
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
- t_notification_config
subdomain: remittance
module: null
sensitivity: normal
name: 汇款通知配置(t_notification_config)
aliases:
- t_notification_config
related_services:
- svc_remittance
related_scenarios: []
---
# 汇款通知配置(t_notification_config)

## 用途
汇款通知配置。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `config_id` | int | PK / AUTO_INC | 主键 |
| `biz_type` | varchar(18) | NOT NULL | 业务类型 |
| `expression` | varchar(255) |  | 通知条件 |
| `notice_method` | varchar(7) | NOT NULL | 通知方式(MAIL-邮件,SMS-短信,NOA-公众号) |
| `notice_party` | varchar(8) | NOT NULL | payer，payee，platform |
| `partner_id` | varchar(20) | NOT NULL | 通知平台方id |
| `subject` | varchar(255) | NOT NULL | 主题 |
| `template_id` | varchar(64) | NOT NULL | SMS和MAIL配置mns模板ID，NOA配置placeholder |
| `icon` | varchar(100) |  | 图标 |
| `notice_rule` | varchar(32) |  | 通知规则，如0,7,25表示第0天，7天，25天各通知一次 |
| `max_retry_times` | int |  | 最大重试次数 |
| `retry_rule` | varchar(64) |  | 重试规则 |
| `status` | char(2) | NOT NULL | 状态(Y - 有效,N - 无效) |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 修改时间 |
| `category` | varchar(20) | NOT NULL | 类型 trade 交易类型, beneficary 受益人类型 |
| `extension` | varchar(500) |  | extension |

## 主键 / 索引
- 主键:(`config_id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

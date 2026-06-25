---
id: tbl_remittance_t_submit_additional_info
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
- t_submit_additional_info
subdomain: remittance
module: null
sensitivity: normal
name: 提交的额外信息(t_submit_additional_info)
aliases:
- t_submit_additional_info
related_services:
- svc_remittance
related_scenarios: []
---
# 提交的额外信息(t_submit_additional_info)

## 用途
提交的额外信息。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | ID;8+9 |
| `order_no` | bigint | NOT NULL | 订单号 |
| `channel_order_no` | varchar(32) |  | 渠道订单号 |
| `session_id` | varchar(32) |  | 渠道sessionId |
| `task_id` | bigint | NOT NULL | Hold Task Id |
| `channel_code` | varchar(12) | NOT NULL | 渠道CODE |
| `biz_type` | varchar(12) | NOT NULL | Sender;Receiver |
| `additional_type` | varchar(7) | NOT NULL | 类型;额外信息类型GW,DL,AML |
| `first_name` | varchar(64) |  | First Name |
| `middle_name` | varchar(100) |  | Middle Name |
| `last_name` | varchar(100) |  | Last Name |
| `father_name` | varchar(100) |  | 父亲名称 |
| `grandfather_name` | varchar(100) |  | 祖父名称 |
| `birth_date` | datetime |  | 生日 |
| `birth_country` | char(2) |  | 出生国 |
| `birth_country_desc` | varchar(64) |  | 出生国名称 |
| `citizenship_country` | char(2) |  | 国籍 |
| `citizenship_country_desc` | varchar(64) |  | 国籍名称 |
| `phone_number` | varchar(64) |  | 手机号 |
| `occupation` | varchar(32) |  | 职业 |
| `general_reason` | varchar(32) |  | 使用原因;为什么使用MG |
| `purpose` | varchar(32) |  | 目的 |
| `relationship` | varchar(32) |  | 关系 |
| `source_of_funds` | varchar(32) |  | 资金来源 |
| `batch_id` | varchar(32) |  | 批次号;打批捞取数据上传sftp |
| `status` | —(DDL未定义) |  |  |
| `extension` | varchar(255) |  | 扩展信息 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

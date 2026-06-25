---
id: tbl_merchant_t_in_app_apply_order
object_type: Table
domain: portal-operations
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (merchant schema) 2026-06-25
tags:
- merchant
- merchant
- t_in_app_apply_order
subdomain: merchant
module: null
sensitivity: normal
name: app申请订单(t_in_app_apply_order)
aliases:
- t_in_app_apply_order
related_services:
- svc_merchant
related_scenarios: []
---
# app申请订单(t_in_app_apply_order)

## 用途
app申请订单。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | 申请id，主键 |
| `merchant_mid` | varchar(50) |  | 商户id |
| `app_id` | bigint | NOT NULL | appId |
| `status` | varchar(32) | NOT NULL | 状态 SUBMITTED 已创建 APPROVED 已通过 REJECTED 已拒绝 |
| `applier_mid` | varchar(32) | NOT NULL | 申请人会员id |
| `error_code` | varchar(50) |  | 错误码 |
| `error_message` | varchar(500) |  | 错误信息 |
| `last_audit_history_id` | bigint |  | 最后审批历史id |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `last_updated_time` | timestamp | NOT NULL | 最后更新时间 |
| `data_version` | bigint | NOT NULL | 数据版本 |
| `oauth_redirect_url` | varchar(300) |  | oauth 重定向 url |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

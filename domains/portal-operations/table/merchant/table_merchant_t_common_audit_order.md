---
id: tbl_merchant_t_common_audit_order
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
- t_common_audit_order
subdomain: merchant
module: null
sensitivity: normal
name: 公共审核订单(t_common_audit_order)
aliases:
- t_common_audit_order
related_services:
- svc_merchant
related_scenarios: []
---
# 公共审核订单(t_common_audit_order)

## 用途
公共审核订单。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | 申请id，主键 |
| `product_code` | varchar(30) | NOT NULL | 产品编码 |
| `product_order_no` | varchar(50) | NOT NULL | 产品订单号 |
| `merchant_mid` | varchar(50) | NOT NULL | 商户id |
| `submit_mid` | varchar(32) | NOT NULL | 提交人会员ID |
| `submit_name` | varchar(200) | NOT NULL | 提交人名称 |
| `submit_time` | timestamp | NOT NULL | 提交时间 |
| `status` | varchar(32) | NOT NULL | 状态  SUBMITTED 已提交 PASSED 已通过 REJECTED 已拒绝 |
| `last_audit_history_id` | bigint |  | 最后审批历史id |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `last_updated_time` | timestamp | NOT NULL | 最后更新时间 |
| `data_version` | bigint | NOT NULL | 数据版本 |
| `audit_mid` | varchar(32) |  | 审批人会员ID |
| `error_code` | varchar(50) |  | 错误码 |
| `error_message` | varchar(500) |  | 错误信息 |
| `business_order_no` | varchar(100) |  | 业务订单号 |
| `audit_type` | varchar(32) |  | 审批类型  OWN 商户审批; OPERATION 运营审批 |
| `audit_result` | varchar(32) |  | 审批结果 PASS 通过 REJECT 拒绝 |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uidx_pcode_porder_no` 唯一 (product_code, product_order_no, merchant_mid)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

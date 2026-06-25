---
id: tbl_ppcenter_t_product_apply_order
object_type: Table
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (ppcenter schema) 2026-06-25
tags:
- ppcenter
- pricing
- t_product_apply_order
subdomain: pricing
module: null
sensitivity: normal
name: 产品申请(t_product_apply_order)
aliases:
- t_product_apply_order
related_services:
- svc_ppcenter
related_scenarios: []
---
# 产品申请(t_product_apply_order)

## 用途
产品申请。属 ppcenter 库,由 [[svc_ppcenter]] 读写。

## 关联关系
- **所属服务**:[[svc_ppcenter]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | 主键id |
| `member_id` | varchar(32) | NOT NULL | 会员id |
| `applicant_member_id` | varchar(32) |  | 申请人会员id |
| `member_name` | varchar(200) | NOT NULL | 商户名称 |
| `package_code` | varchar(32) |  | 产品集code |
| `status` | varchar(2) | NOT NULL | I=待审核，P=处理中，S=审核成功，R=审核拒绝 |
| `contract_no` | varchar(64) |  | 合同编号 |
| `memo` | varchar(255) |  | 备注 |
| `extension` | varchar(255) |  | 扩展参数 |
| `gmt_create` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 创建时间 |
| `gmt_modify` | timestamp |  | 修改时间 |
| `gmt_effective` | timestamp |  | 生效时间 |
| `gmt_invalid` | timestamp |  | 失效时间 |
| `applicant_name` | varchar(126) |  | 申请人名称 |
| `applicant_address` | varchar(255) |  | 异常通知地址 |
| `package_version` | varchar(64) |  | 产品集版本 |
| `package_name` | varchar(64) |  | 产品集名称 |
| `package_type` | varchar(15) |  | PARTNER_MCHT:平台方商户;PAYEE_MCHT:收款方商户 |
| `sec_merchant_id` | varchar(32) |  | 二级商户号 |
| `payee_id` | varchar(20) |  | 收款方商户 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_member_id` (member_id, gmt_create)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

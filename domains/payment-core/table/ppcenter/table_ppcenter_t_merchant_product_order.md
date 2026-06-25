---
id: tbl_ppcenter_t_merchant_product_order
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
- t_merchant_product_order
subdomain: pricing
module: null
sensitivity: normal
name: 商户配置记录(t_merchant_product_order)
aliases:
- t_merchant_product_order
related_services:
- svc_ppcenter
related_scenarios: []
---
# 商户配置记录(t_merchant_product_order)

## 用途
商户配置记录。属 ppcenter 库,由 [[svc_ppcenter]] 读写。

## 关联关系
- **所属服务**:[[svc_ppcenter]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC |  |
| `member_id` | varchar(32) | NOT NULL | 平台号 |
| `status` | varchar(1) | NOT NULL | 表示信息入库成功 |
| `memo` | varchar(128) |  | 备注 |
| `gmt_create` | timestamp | NOT NULL | 创建时间 |
| `gmt_modify` | timestamp | 默认 CURRENT_TIMESTAMP | 修改时间 |
| `gmt_effective` | timestamp | NOT NULL | 生效时间 |
| `gmt_invalid` | timestamp | NOT NULL | 失效时间 |
| `biz_product_code` | varchar(64) |  | 产品码 |
| `step` | varchar(2) |  | step:P，费率，A，表示接口鉴权，G，表示网关接口组，B，表示账单 |
| `extension` | varchar(255) |  | 扩展参数 |
| `apply_id` | int |  | 申请id |
| `version` | varchar(32) |  | 版本号 |
| `package_code` | varchar(64) |  | 产品集code |
| `package_type` | varchar(15) |  | PARTNER_MCHT:平台方商户;PAYEE_MCHT:收款方商户 |
| `package_name` | varchar(64) |  | 产品集名称 |
| `package_version` | varchar(32) |  | 产品集版本 |
| `sec_merchant_id` | varchar(32) |  | 二级商户号 |
| `payee_id` | varchar(20) |  | 收款方商户 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `inx_apply_id` (apply_id)
  - `inx_memberid` (member_id)
  - `inx_payee_id` (payee_id)
  - `inx_sec_merchant_id` (sec_merchant_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

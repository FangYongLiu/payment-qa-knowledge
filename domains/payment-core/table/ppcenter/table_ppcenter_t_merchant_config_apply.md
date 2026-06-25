---
id: tbl_ppcenter_t_merchant_config_apply
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
- t_merchant_config_apply
subdomain: pricing
module: null
sensitivity: normal
name: 商户配置申请(t_merchant_config_apply)
aliases:
- t_merchant_config_apply
related_services:
- svc_ppcenter
related_scenarios: []
---
# 商户配置申请(t_merchant_config_apply)

## 用途
商户配置申请。属 ppcenter 库,由 [[svc_ppcenter]] 读写。

## 关联关系
- **所属服务**:[[svc_ppcenter]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | 主键 |
| `member_id` | varchar(32) | NOT NULL | 商户号 |
| `biz_product_code` | varchar(64) | NOT NULL | 业务产品码 |
| `package_name` | varchar(64) | NOT NULL | 产品名称 |
| `config_type` | varchar(255) | NOT NULL | 修改类型 |
| `status` | varchar(255) | NOT NULL | 状态 |
| `applicant_name` | varchar(255) | NOT NULL | 申请人 |
| `gmt_create` | timestamp | NOT NULL | 创建时间 |
| `gmt_modify` | timestamp | 默认 CURRENT_TIMESTAMP | 修改时间 |
| `product_order_id` | int(16) | NOT NULL | 开通历史记录id |
| `payee_id` | varchar(20) |  | 收款方商户 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

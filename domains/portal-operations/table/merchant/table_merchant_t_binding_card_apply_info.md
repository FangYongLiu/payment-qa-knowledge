---
id: tbl_merchant_t_binding_card_apply_info
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
- t_binding_card_apply_info
subdomain: merchant
module: null
sensitivity: normal
name: 商户绑定银行卡信息(t_binding_card_apply_info)
aliases:
- t_binding_card_apply_info
related_services:
- svc_merchant
related_scenarios: []
---
# 商户绑定银行卡信息(t_binding_card_apply_info)

## 用途
商户绑定银行卡信息。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | order id |
| `merchant_creation_id` | bigint | NOT NULL | 商户订单ID |
| `merchant_mid` | varchar(20) |  | 商户mid |
| `admin_mid` | varchar(20) |  | 商户管理人mid |
| `holder_name` | varchar(255) |  | 卡持有人 |
| `account_no` | varchar(32) |  | 卡号 |
| `iban_no` | varchar(34) |  | iban |
| `bank_name` | varchar(100) |  | 银行名称 |
| `bank_code` | varchar(50) |  | 银行编码 |
| `swift_code` | varchar(30) |  | swift code |
| `country_code` | varchar(10) |  | 国家代码 |
| `city_code` | varchar(32) |  | City Code |
| `city_name` | varchar(64) |  | 城市名称 |
| `beneficiary_address` | varchar(300) |  | 收款人地址 |
| `bank_branch` | varchar(100) |  | 支行 |
| `currency` | char(3) |  | 币种 |
| `intermediary_bank` | varchar(100) |  | 中间行 |
| `beneficiary_type` | varchar(12) |  | 受益人类型 |
| `params` | varchar(500) |  | 扩展信息 |
| `official_letter_path` | varchar(200) |  | 授权函（Official Letter） |
| `bank_letter_path` | varchar(200) |  | 银行证明或流水(Bank Letter/Statement) |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `last_updated_time` | timestamp | NOT NULL | 最后更新时间 |
| `data_version` | bigint | NOT NULL | 数据版本 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

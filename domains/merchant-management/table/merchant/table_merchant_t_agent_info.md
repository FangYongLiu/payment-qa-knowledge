---
id: tbl_merchant_t_agent_info
object_type: Table
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (merchant schema) 2026-06-25
tags:
- merchant
- merchant
- t_agent_info
subdomain: merchant
module: null
sensitivity: normal
name: 代理商信息(t_agent_info)
aliases:
- t_agent_info
related_services:
- svc_merchant
related_scenarios: []
---
# 代理商信息(t_agent_info)

## 用途
代理商信息。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | order id |
| `merchant_contract_path` | varchar(200) |  | 商户合同路径 |
| `agent_merchant_mid` | varchar(50) | NOT NULL | 代理公司商户id |
| `agent_mid` | varchar(50) | NOT NULL | 代理人id |
| `holder_name` | varchar(255) |  | 卡持有人 |
| `account_no` | varchar(50) |  | 卡号 |
| `iban_no` | varchar(50) |  | iban |
| `bank_name` | varchar(200) |  | 银行名称 |
| `bank_code` | varchar(50) |  | 银行编码 |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `last_updated_time` | timestamp | NOT NULL | 最后更新时间 |
| `data_version` | bigint | NOT NULL | 数据版本 |
| `merchant_onboard_contract_path` | varchar(200) |  | 商户登记合同 |
| `swift_code` | varchar(30) |  | swift code |
| `country_code` | varchar(10) |  | 国家代码 |
| `city_name` | varchar(200) |  | 城市名称 |
| `beneficiary_address` | varchar(300) |  | 收款人地址 |
| `bank_branch` | varchar(200) |  | 支行 |
| `currency` | varchar(3) |  | 币种 |
| `params` | varchar(500) |  | 扩展信息 |
| `intermediary_bank` | varchar(100) |  | 中间行 |
| `beneficiary_type` | varchar(32) |  | 受益人类型 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

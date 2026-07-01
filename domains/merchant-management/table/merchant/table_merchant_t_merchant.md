---
id: tbl_merchant_t_merchant
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
- t_merchant
subdomain: merchant
module: null
sensitivity: normal
name: 商户(t_merchant)
aliases:
- t_merchant
related_services:
- svc_merchant
related_scenarios: []
---
# 商户(t_merchant)

## 用途
商户。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | 主键 |
| `mid` | varchar(50) | NOT NULL | 商户id |
| `name` | varchar(100) | NOT NULL | 商户简称 |
| `status` | varchar(32) | NOT NULL | 状态 CREATED 已创建 |
| `licence_photo_path` | varchar(200) | NOT NULL | 营业执照路径 |
| `contact_name` | varchar(64) |  | 联系人名称 |
| `contact_mobile` | varchar(20) |  | 联系人手机号 |
| `contact_email` | varchar(100) |  | Email address of the primary contact |
| `admin_mid` | varchar(32) | NOT NULL | 管理员id |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `last_updated_time` | timestamp | NOT NULL | 最后更新时间 |
| `data_version` | bigint | NOT NULL | 数据版本 |
| `id_front_photo_path` | varchar(200) |  | id卡正面照片路径 |
| `id_back_photo_path` | varchar(200) |  | id卡背面照片路径 |
| `group_id` | bigint |  | 集团ID |
| `branch_id` | bigint |  | 分公司ID |
| `commercial_activities` | varchar(300) |  | 经营范围 |
| `tax_reg_certificate_path` | varchar(200) |  | 税务登记证书路径 |
| `copy_of_memorandum_path` | varchar(200) |  | 公司章程 |
| `merchant_contract_path` | varchar(200) |  | 商户合同路径 |
| `agent_merchant_mid` | varchar(50) |  | 代理商户ID |
| `agent_mid` | varchar(50) |  | 代理会员ID |
| `business_type` | varchar(50) |  | 业务类型 AGENT 代理商 MERCHANT 普通商户 |
| `business_name` | varchar(300) |  | 商户全称 |
| `tax_reg_no` | varchar(50) |  | 税务登记号 |
| `business_address` | varchar(300) |  | 公司地址 |
| `business_state` | varchar(100) |  | 公司所在州 |
| `icon_path` | varchar(200) |  | 商户icon |
| `website` | varchar(200) |  | 商户网址 |
| `merchant_type` | varchar(50) |  | 商户类型 EXTERNAL 外部商户 INTERNAL 内部商户 |
| `country` | varchar(100) |  | 国家 |
| `category` | varchar(200) |  | 商户种类 |
| `bank_statement` | varchar(200) |  | bank staetment |
| `poa_or_noc` | varchar(200) |  | poa or noc |
| `country_code` | varchar(10) |  | 国家代码 |
| `create_source` | varchar(20) |  | 来源 |
| `botim_business_type` | varchar(30) |  | botim store 业务类型 stand alone、chain |
| `license_expire_time` | timestamp |  | 营业执照过期时间 |
| `doc_expire_time` | timestamp |  | 证件过期时间 |
| `director` | varchar(100) |  | 董事 |
| `share_holder` | varchar(100) |  | 股东 |
| `beneficial_owner` | varchar(100) |  | 法定受益人 |
| `authorized_signer` | varchar(100) |  | 法人 |
| `biz_org_structure` | varchar(50) |  | 法律类型（Legal Type） |
| `screening_result_path` | varchar(200) |  | 公司名称扫描结果文件路径 |
| `merchant_onboard_contract_path` | varchar(100) |  | 商户登记合同 |
| `trade_license_no` | varchar(40) |  | 营业执照号码 |
| `issuing_license_authority` | varchar(100) |  | 营业执照颁发机构 |
| `license_issue_date` | datetime |  | 营业执照生效日期 |
| `incorporation_date` | datetime |  | 公司成立时间 |
| `company_ownership_path` | varchar(200) |  | 公司所有权(营业执照,MOA,NOC,股东登记摘要文件等)-股东(合伙人) |
| `industry` | varchar(100) |  | 行业 |
| `aplus_online_approve_result` | varchar(20) |  | 线上报备A+产品 |
| `compliance_level` | varchar(20) |  | 商户合规等级 |
| `aplus_product_apply_result` | varchar(20) |  | 报备状态 |
| `arabic_name` | varchar(300) |  | arabic name |
| `referrer_flag` | varchar(20) |  | Referrer Flag |
| `referrer_mid` | varchar(50) |  | Referrer Merchant Mid |
| `risk_comments` | varchar(500) |  | Risk Comments(风控备注) |
| `jurisdiction` | varchar(50) |  | High-Risk Jurisdiction Involvement |
| `monthly_turnover` | varchar(50) |  | Monthly Turnover |
| `payment_method` | varchar(50) |  | Payment Methods |
| `delivery_channel` | varchar(50) |  | Delivery Channels |
| `establishment_card_path` | varchar(200) |  | Establishment card |
| `industry_type` | varchar(50) |  | Industry Type |
| `sanctions` | varchar(50) |  | Sanctions Screening |
| `adv_pep` | varchar(50) |  | ADV PEP Screening |
| `ubo_nationality` | varchar(50) |  | UBO Nationality |
| `biz_overview` | varchar(50) |  | Business Profile Overview |
| `product_service` | varchar(50) |  | Product Services |
| `risk_level` | varchar(50) |  | Onboarding Risk Assessment |
| `risk_score` | varchar(16) |  | Risk Score |
| `is_website_applicable` | tinyint |  | Is website info available for merchant |
| `signed_onboarding_form` | varchar(200) |  | Path or reference to the signed onboarding form |
| `is_pay_facs` | tinyint(1) | NOT NULL / 默认 0 | Indicates if the merchant is a PayFac |
| `company_contact_number` | varchar(50) |  | Contact number |
| `company_contact_email` | varchar(100) |  | Email address for company communications |
| `monthly_expected_transaction_count` | int |  | Total Monthly Expected Number of Transactions |
| `monthly_expected_sales_volume` | decimal(15,2) |  | Total Monthly Expected Transaction Sales Volume |
| `expected_transaction_value` | decimal(15,2) |  | Expected Transaction Value |
| `average_transaction_value` | decimal(15,2) |  | Average Transaction Value |
| `highest_transaction_value` | decimal(15,2) |  | Highest Transaction Value |
| `mcc_description` | varchar(500) |  | Business category description |
| `mcc_percentage` | varchar(500) |  | Product Percentage |
| `block_flag` | varchar(20) |  | Merchant block flag status |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_merchant_id` 唯一 (mid)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

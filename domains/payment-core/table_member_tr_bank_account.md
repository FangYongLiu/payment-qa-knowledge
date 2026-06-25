---
id: tbl_member_tr_bank_account
object_type: Table
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (member schema) 2026-06-25
tags:
- member
- account
- tr_bank_account
subdomain: account
module: null
sensitivity: sensitive
name: 个人银行卡信息表(tr_bank_account)
aliases:
- tr_bank_account
related_services:
- svc_member
related_scenarios: []
---

# 个人银行卡信息表(tr_bank_account)

## 用途
个人银行卡信息表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `ID` | decimal(28) | PK / NOT NULL | 主键 |
| `MEMBER_ID` | varchar(32) | NOT NULL | 会员ID |
| `BANK_ID` | varchar(10) |  | 银行编号 |
| `BANK_NAME` | varchar(50) |  | 银行名称 |
| `BANK_ACCOUNT_NO` | varchar(50) |  | 银行卡号 |
| `BANK_ACCOUNT_NAME` | varchar(255) |  | 户名 |
| `CARD_ATTRIBUTE` | decimal(8) | NOT NULL | 卡属性(0对公 1对私) |
| `CARD_TYPE` | decimal(8) |  | 卡类型(1借记卡 2信用卡,3存折,4其它) |
| `COUNTRY_CODE` | varchar(16) |  | 国家编码 |
| `IS_VERIFIED` | decimal(8) |  | 认证状态(0未认证 1已认证) |
| `STATUS` | decimal(8) | NOT NULL | 状态(0失效  1正常 2锁定) |
| `CREATE_TIME` | timestamp |  | 建立时间 |
| `UPDATE_TIME` | timestamp |  | 更新时间 |
| `MOBILE_NO` | varchar(64) |  | 手机号 |
| `CHANNEL_CODE` | varchar(64) |  | 渠道编号 |
| `iban` | varchar(50) |  | IBAN号 |
| `card_no` | varchar(100) |  | 卡号 |
| `CARD_ORGANIZATION` | tinyint(2) |  | 0-Other,1-VISA,2-Master,3-Amex,4-UnionPay |
| `CARD_CATEGORY` | tinyint |  | 卡类别 |
| `OUT_ACCOUNT_TOKEN` | varchar(50) |  | 外部账户Token |
| `CURRENCY` | varchar(3) |  | 币种 |
| `SWIFT_CODE` | varchar(11) |  | 银行识别码 |
| `EMAIL` | varchar(55) |  | 邮箱 |
| `archive_date` | datetime |  | 归档日期 |
| `identity` | varchar(32) |  | NYU学生ID |

## 主键 / 索引
- 主键:(`ID`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- ⚠️ 含敏感字段(身份证/姓名/卡号/IBAN/密码/手机/邮箱/照片等),**密文落库 + 对象级访问控制**。
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

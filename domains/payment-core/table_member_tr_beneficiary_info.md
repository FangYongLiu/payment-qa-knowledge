---
id: tbl_member_tr_beneficiary_info
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
- beneficiary
- tr_beneficiary_info
subdomain: beneficiary
module: null
sensitivity: restricted
name: 受益人卡信息表(tr_beneficiary_info)
aliases:
- tr_beneficiary_info
related_services:
- svc_member
related_scenarios: []
---

# 受益人卡信息表(tr_beneficiary_info)

## 用途
受益人卡信息表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint(32) | PK / NOT NULL | 主键 |
| `member_id` | varchar(32) | NOT NULL | 会员ID |
| `beneficiary_type` | varchar(20) | NOT NULL | 受益人类型 |
| `holder_name` | varchar(125) | NOT NULL | 受益人姓名 |
| `country_code` | varchar(35) | NOT NULL | 国家码 |
| `account_no` | varchar(35) | NOT NULL | 受益人账户 |
| `bank_code` | varchar(35) |  | 银行code |
| `bank_name` | varchar(55) |  | 银行名称 |
| `intermediary_bank` | varchar(35) |  | 中间行BIC的code |
| `routing_code` | varchar(35) |  | 银行routingCode |
| `pay_attribute` | varchar(35) | NOT NULL | 支付属性 |
| `card_category` | varchar(25) | NOT NULL | 卡类别 |
| `alias` | varchar(55) |  | 别名 |
| `currency` | varchar(3) | NOT NULL | 币种 |
| `status` | varchar(10) | NOT NULL | 状态（失效，正常，锁定，未激活） |
| `extension` | varchar(500) |  | 拓展字段（json格式） |
| `active_time` | datetime | NOT NULL | 激活时间 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- ⚠️ 含敏感字段(身份证/姓名/卡号/IBAN/密码/手机/邮箱/照片等),**密文落库 + 对象级访问控制**。
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

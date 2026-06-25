---
id: tbl_member_tm_merchant_user_card
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
- card-binding
- tm_merchant_user_card
subdomain: card-binding
module: null
sensitivity: sensitive
name: 商户下用户绑卡信息表(tm_merchant_user_card)
aliases:
- tm_merchant_user_card
related_services:
- svc_member
related_scenarios: []
---

# 商户下用户绑卡信息表(tm_merchant_user_card)

## 用途
商户下用户绑卡信息表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键id |
| `member_id` | varchar(20) | NOT NULL | 会员id |
| `identity` | varchar(64) |  | 外部用户标识 |
| `bank_code` | varchar(20) |  | 银行CODE |
| `bank_name` | varchar(255) |  | 银行名称 |
| `holder_name` | varchar(255) |  | 用户名 |
| `card_no` | varchar(64) |  | 卡号 |
| `card_type` | varchar(32) |  | 卡类型 |
| `channel_code` | varchar(20) |  | 绑卡渠道 |
| `activate_time` | timestamp |  | 激活时间 |
| `is_verified` | char |  | 是否已认证 |
| `expiry_time` | varchar(12) |  | 失效时间 |
| `card_org` | varchar(20) |  | 卡组织 |
| `country_code` | varchar(2) |  | 国家code |
| `email` | varchar(64) |  | 邮箱 |
| `status` | tinyint(2) |  | 状态 |
| `extension` | varchar(255) |  | 扩展信息 |
| `archive_date` | datetime |  | 归档日期 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- ⚠️ 含敏感字段(身份证/姓名/卡号/IBAN/密码/手机/邮箱/照片等),**密文落库 + 对象级访问控制**。
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

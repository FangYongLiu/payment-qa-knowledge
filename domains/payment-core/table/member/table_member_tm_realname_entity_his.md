---
id: tbl_member_tm_realname_entity_his
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
- kyc-verify
- tm_realname_entity_his
subdomain: kyc-verify
module: null
sensitivity: restricted
name: Real name info history table(tm_realname_entity_his)
aliases:
- tm_realname_entity_his
related_services:
- svc_member
related_scenarios: []
---

# Real name info history table(tm_realname_entity_his)

## 用途
Real name info history table。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `his_id` | int |  | Primary key |
| `entity_id` | bigint | PK / NOT NULL | Real name |
| `member_id` | varchar(20) | NOT NULL | Member id |
| `id_number` | varchar(110) | NOT NULL | ID number |
| `real_name` | varchar(200) | NOT NULL | Real name |
| `nationality_code` | char(3) |  | Nationality alpha2 code |
| `status` | decimal(8) |  | Status(1-Normal,9-Invalid) |
| `partner_id` | varchar(25) |  | Partner Id |
| `expire_time` | timestamp |  | Expire time |
| `verified_time` | timestamp |  | Verified time |
| `last_renew_time` | timestamp |  | Last renew time |
| `eid_front` | varchar(55) |  | Eid front |
| `eid_back` | varchar(55) |  | Eid back |
| `create_time` | timestamp | NOT NULL | Create time |
| `update_time` | timestamp | NOT NULL | Update time |

## 主键 / 索引
- 主键:(`entity_id`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- ⚠️ 含敏感字段(身份证/姓名/卡号/IBAN/密码/手机/邮箱/照片等),**密文落库 + 对象级访问控制**。
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

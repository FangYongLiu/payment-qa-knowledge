---
id: tbl_member_tr_beneficiary_city
object_type: Table
domain: activation
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (member schema) 2026-06-25
tags:
- member
- beneficiary
- tr_beneficiary_city
subdomain: beneficiary
module: null
sensitivity: normal
name: Beneficiary City Table(tr_beneficiary_city)
aliases:
- tr_beneficiary_city
related_services:
- svc_member
related_scenarios: []
---

# Beneficiary City Table(tr_beneficiary_city)

## 用途
Beneficiary City Table。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint(32) | PK | 主键 |
| `country_code` | varchar(5) | NOT NULL | Country Code |
| `city_code` | varchar(25) | NOT NULL | City Code |
| `city_name` | varchar(155) | NOT NULL | City Name |
| `state_code` | varchar(25) |  | State Code |
| `state_name` | varchar(155) |  | State Name |
| `enable` | char | NOT NULL | Is Enable (Y/N) |
| `create_time` | timestamp | NOT NULL | Create Time |
| `update_time` | timestamp | NOT NULL | Update Time |

## 主键 / 索引
- 主键:(`id`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

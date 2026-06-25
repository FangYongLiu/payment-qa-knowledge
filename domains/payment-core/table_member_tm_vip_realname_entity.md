---
id: tbl_member_tm_vip_realname_entity
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
- tm_vip_realname_entity
subdomain: kyc-verify
module: null
sensitivity: restricted
name: VIP会员真实姓名信息表(tm_vip_realname_entity)
aliases:
- tm_vip_realname_entity
related_services:
- svc_member
related_scenarios: []
---

# VIP会员真实姓名信息表(tm_vip_realname_entity)

## 用途
VIP会员真实姓名信息表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK | 主键ID |
| `member_id` | varchar(20) | NOT NULL | 会员ID |
| `id_number` | varchar(110) | NOT NULL | 身份证号 |
| `real_name` | varchar(200) | NOT NULL | 真实姓名 |
| `nationality_code` | char(3) |  | 国家alpha2 |
| `status` | tinyint |  | 状态(1-正常,9-已作废) |
| `source` | varchar(25) |  | 实名来源 |
| `partner_id` | varchar(15) |  | 平台ID |
| `finish_way` | varchar(15) |  | 完成方式，如：offline / online |
| `attachments` | varchar(750) |  | 照片等附件信息，JSON格式 |
| `create_time` | timestamp |  | 建立时间 |
| `update_time` | timestamp |  | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- ⚠️ 含敏感字段(身份证/姓名/卡号/IBAN/密码/手机/邮箱/照片等),**密文落库 + 对象级访问控制**。
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

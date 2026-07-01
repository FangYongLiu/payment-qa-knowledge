---
id: tbl_member_tr_member_public_key
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
- operator-security
- tr_member_public_key
subdomain: operator-security
module: null
sensitivity: restricted
name: 会员公钥表(tr_member_public_key)
aliases:
- tr_member_public_key
related_services:
- svc_member
related_scenarios: []
---

# 会员公钥表(tr_member_public_key)

## 用途
会员公钥表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键id |
| `member_id` | varchar(32) | NOT NULL | 会员id |
| `partner_id` | varchar(32) | NOT NULL | 平台方 |
| `host_app` | varchar(16) | NOT NULL | 宿主App |
| `platform` | varchar(16) | NOT NULL | 平台类型 |
| `device_id` | varchar(64) | NOT NULL | 设备ID |
| `algorithm` | varchar(32) | NOT NULL | 算法 |
| `cert_type` | varchar(32) | NOT NULL | 密钥类型 |
| `cert` | varchar(4000) | NOT NULL | 密钥 |
| `enable_flag` | char | NOT NULL | 启用标识 |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `updated_time` | timestamp | NOT NULL | 修改时间 |
| `memo` | varchar(255) |  | 备注信息 |

## 主键 / 索引
- 主键:(`id`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- ⚠️ 含敏感字段(身份证/姓名/卡号/IBAN/密码/手机/邮箱/照片等),**密文落库 + 对象级访问控制**。
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

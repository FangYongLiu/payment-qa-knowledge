---
id: tbl_member_tr_member_kyc_level
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
- kyc-verify
- tr_member_kyc_level
subdomain: kyc-verify
module: null
sensitivity: normal
name: 会员KYC等级表(tr_member_kyc_level)
aliases:
- tr_member_kyc_level
related_services:
- svc_member
related_scenarios: []
---

# 会员KYC等级表(tr_member_kyc_level)

## 用途
会员KYC等级表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK | 自增id |
| `member_id` | varchar(32) | NOT NULL | 会员id |
| `source` | varchar(20) |  | Kyc来源 |
| `kyc_type` | varchar(20) |  | Kyc类型 EID PASSPORT BANK_CARD |
| `kyc_level` | tinyint(2) |  | Kyc等级 0:cdd0 1:cdd1 2:cdd2 |
| `status` | varchar(15) |  | 状态 有效 vaild 无效 invaild |
| `invalid_time` | timestamp |  | 失效时间 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |
| `extension` | varchar(64) |  | 扩展字段 |

## 主键 / 索引
- 主键:(`id`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

---
id: tbl_kyc_tm_invitation_code
object_type: Table
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-24'
source_type: DB DDL
source_ref: DataGrip DDL export (kyc schema) 2026-06-24
tags:
- kyc
- invitation
- tm_invitation_code
subdomain: invitation
module: null
sensitivity: restricted
name: 用户kyc邀请码(tm_invitation_code)
aliases:
- tm_invitation_code
related_services:
- svc_kyc
related_scenarios: []
---

# 用户kyc邀请码(tm_invitation_code)

## 用途
**KYC 邀请码表**:实名邀请码及归属人(code_owner_id)、类别、状态、失败原因。`relation_id` 关联流程。

## 关联关系
- **所属服务**:[[svc_kyc]](gp078_kyc,= frontmatter `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补(暂无直接关联场景对象)。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键ID |
| `relation_id` | bigint |  | 流程记录关联ID |
| `member_id` | varchar(32) | NOT NULL | 会员ID |
| `code_owner_id` | varchar(32) | NOT NULL | 邀请码归属人ID |
| `invitation_code` | varchar(255) | NOT NULL | 邀请码 |
| `invitation_category` | varchar(55) |  | 邀请码类别 |
| `status` | varchar(2) | NOT NULL | 状态（是否有效） |
| `error_msg` | varchar(255) |  | 邀请失败错误描述 |
| `sub_status` | varchar(20) |  | 邀请码子状态 |
| `invite_type` | varchar(32) |  | 邀请类型 |
| `invite_sub_type` | varchar(32) |  | 邀请子类型 |
| `mobile` | varchar(32) |  | 手机密文和掩码 |
| `extension` | varchar(255) |  | 拓展字段 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |
| `memo` | varchar(64) |  | 备注说明 |

## 主键 / 索引
- 主键:(`id`)
- 索引 `idx_ctm`:(`create_time`)
- 索引 `idx_mid`:(`member_id`)

## 校验点(QA 关注)
- `status` 有效性与 `error_msg`;邀请码唯一。
- invite_type/sub_type 与业务对应;mobile 密文。

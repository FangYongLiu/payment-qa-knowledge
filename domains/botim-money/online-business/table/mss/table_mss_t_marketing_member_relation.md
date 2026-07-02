---
id: tbl_mss_t_marketing_member_relation
object_type: Table
name: 营销邀请关系表 (t_marketing_member_relation)
aliases: [t_marketing_member_relation, mss.t_marketing_member_relation]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mss schema DDL
tags: [online-business, mss]
sensitivity: normal
related_services: []
---

# 营销邀请关系表 (t_marketing_member_relation)

## 用途
物理表 `mss.t_marketing_member_relation`,主键 `rlt_id`。营销邀请关系表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `rlt_id` | bigint | 主键 |
| `activity_code` | varchar(64) | 活动code |
| `inviter_mid` | varchar(32) | 邀请人 |
| `invitee_mid` | varchar(32) | 被邀请人 · 可空 |
| `rlt_keyword` | varchar(32) | 营销关系关键字 |
| `keyword_type` | varchar(32) | 关键字类型 |
| `rlt_status` | varchar(16) | 关联关系状态 |
| `rlt_type` | varchar(16) | 分享关系类型 |
| `rlt_source` | varchar(16) | 分享关系来源 |
| `effective_time` | timestamp | 生效时间 · 可空 |
| `expire_time` | timestamp | 过期时间 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 更新时间 |
| `invitee_props` | varchar(200) | 被邀请人信息 · 可空 |
| `inviter_props` | varchar(200) | 邀请人信息 · 可空 |

## 主键 / 索引
- 主键:`rlt_id`
- `idx_tmmr_contact`:rlt_keyword
- `idx_tmmr_mid`:inviter_mid

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

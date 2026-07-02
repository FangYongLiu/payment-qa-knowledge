---
id: tbl_scoupon_t_invitation_record
object_type: Table
name: 邀请记录表 (t_invitation_record)
aliases: [t_invitation_record, scoupon.t_invitation_record]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: scoupon schema DDL
tags: [marketing, scoupon]
sensitivity: normal
related_services: []
---

# 邀请记录表 (t_invitation_record)

## 用途
物理表 `scoupon.t_invitation_record`,主键 `id`。邀请记录表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 |
| `inviter` | varchar(32) | 邀请人id · 可空 |
| `invitee` | varchar(32) | 被邀请人id · 可空 |
| `status` | varchar(32) | 状态 已绑定:BIND;已领取:SUCCESS;过期:EXPIRED;失败:FAILURE · 可空 |
| `invitee_mobile` | varchar(32) | 被邀请人手机号 · 可空 |
| `notify_flag` | varchar(32) | 是否已提醒 · 可空 |
| `expired_time` | timestamp | 领取过期时间 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 修改时间 |
| `extension` | varchar(255) | 额外信息 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_created_time`:created_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

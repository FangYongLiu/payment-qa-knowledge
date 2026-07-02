---
id: tbl_ups_t_ups_set_habit
object_type: Table
name: 用户使用习惯表 (t_ups_set_habit)
aliases: [t_ups_set_habit, ups.t_ups_set_habit]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ups schema DDL
tags: [activation, ups]
sensitivity: normal
related_services: []
---

# 用户使用习惯表 (t_ups_set_habit)

## 用途
物理表 `ups.t_ups_set_habit`,主键 `id`。用户使用习惯表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 |
| `member_id` | varchar(32) | 会员ID |
| `partner_id` | varchar(32) | 商户ID |
| `nick_name` | varchar(64) | 昵称 · 可空 |
| `head_url` | varchar(255) | 头像地址 · 可空 |
| `lang` | varchar(8) | 语言 |
| `sign_note` | varchar(255) | 签名备注 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- `uk_member_id_partner_id`:member_id, partner_id (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

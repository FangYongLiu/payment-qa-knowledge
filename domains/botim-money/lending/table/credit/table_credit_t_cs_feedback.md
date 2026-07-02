---
id: tbl_credit_t_cs_feedback
object_type: Table
name: 用户反馈 (t_cs_feedback)
aliases: [t_cs_feedback, credit.t_cs_feedback]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: credit schema DDL
tags: [lending, credit]
sensitivity: normal
related_services: []
---

# 用户反馈 (t_cs_feedback)

## 用途
物理表 `credit.t_cs_feedback`,主键 `id`。用户反馈。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `user_id` | varchar(32) | 用户id |
| `email` | varchar(255) | 邮箱 · 可空 |
| `category` | varchar(50) | 类别 |
| `message` | varchar(1000) | 消息 |
| `best_contact_time` | varchar(50) | 联系时间 |
| `attachment` | varchar(255) | 附件地址 |
| `subcategory` | varchar(64) | 子类别 · 可空 |
| `mobile` | varchar(50) | 手机号 |
| `create_time` | timestamp | 创建日期 |
| `update_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `idx_create_time`:create_time
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_shortlink_t_shortcode_record
object_type: Table
name: 分享口令记录表 (t_shortcode_record)
aliases: [t_shortcode_record, shortlink.t_shortcode_record]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: shortlink schema DDL
tags: [marketing, shortlink]
sensitivity: normal
related_services: []
---

# 分享口令记录表 (t_shortcode_record)

## 用途
物理表 `shortlink.t_shortcode_record`,主键 `id`。分享口令记录表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `short_link` | varchar(255) | 短链接 |
| `short_code` | varchar(25) | 临时口令码 |
| `short_code_type` | varchar(25) | 口令码类型 |
| `title` | varchar(500) | 展示标题 · 可空 |
| `content` | varchar(700) | 展示内容 · 可空 |
| `show_pic` | varchar(500) | 展示图片 · 可空 |
| `nick_name` | varchar(255) | 展示昵称 · 可空 |
| `head_portrait` | varchar(500) | 展示头像 · 可空 |
| `member_id` | varchar(25) | 分享人MID · 可空 |
| `partner_id` | varchar(25) | 平台ID · 可空 |
| `action_type` | varchar(25) | 跳转类型 · 可空 |
| `dialog_type` | varchar(30) | 弹窗类型 · 可空 |
| `status` | char | 状态（Y：有效，N：无效） |
| `expiry_time` | datetime | 有效期 · 可空 |
| `memo` | varchar(800) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- `idx_short_code`:short_code (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

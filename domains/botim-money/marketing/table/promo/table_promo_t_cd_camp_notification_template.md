---
id: tbl_promo_t_cd_camp_notification_template
object_type: Table
name: notification template (t_cd_camp_notification_template)
aliases: [t_cd_camp_notification_template, promo.t_cd_camp_notification_template]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: promo schema DDL
tags: [marketing, promo]
sensitivity: normal
related_services: []
---

# notification template (t_cd_camp_notification_template)

## 用途
物理表 `promo.t_cd_camp_notification_template`,主键 `id`。notification template。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | ulid |
| `source` | varchar(20) | Kyc|Remittance|Default |
| `template` | varchar(20) | tReferee|Referrer|Default |
| `title` | varchar(127) | title |
| `sub_title` | varchar(127) | subject |
| `image_url` | varchar(255) | image url |
| `content` | varchar(255) | content · 可空 |
| `default_link` | varchar(255) | default link · 可空 |
| `expire_time` | mediumtext | expire time · 可空 |
| `left_button_text` | varchar(20) | left button text · 可空 |
| `left_button_link` | varchar(255) | left button link · 可空 |
| `right_button_text` | varchar(20) | right button text · 可空 |
| `right_button_link` | varchar(255) | right button link · 可空 |
| `icon_url` | varchar(255) | icon url · 可空 |
| `is_deleted` | tinyint(1) | is deleted |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_activity_t_page_record
object_type: Table
name: 为用户配置的开屏页地址 (t_page_record)
aliases: [t_page_record, activity.t_page_record]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: activity schema DDL
tags: [marketing, activity]
sensitivity: normal
related_services: []
---

# 为用户配置的开屏页地址 (t_page_record)

## 用途
物理表 `activity.t_page_record`,主键 `id`。为用户配置的开屏页地址。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `rtr_id` | int | 对应t_recall_trigger_record的id |
| `member_id` | bigint(32) | 用户id |
| `status` | smallint | 待补 |
| `page_url` | varchar(128) | page页面 |
| `display_limit` | int | 最高展示次数 |
| `button_click_limit` | int | 最高button点击次数 |
| `rcp_invalid_time` | timestamp | 触发为用户配置page_url 营销任务的失效时间 · 可空 |
| `rcp_valid_time` | timestamp | 触发为用户配置page_url 营销任务的生效时间 · 可空 |
| `rcp_create_time` | timestamp | 触发为用户配置page_url 营销任务的创建时间 · 可空 |
| `product` | smallint | 1、cashnow，2、paylater，3、wecredit |
| `create_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `ix_mid`:member_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

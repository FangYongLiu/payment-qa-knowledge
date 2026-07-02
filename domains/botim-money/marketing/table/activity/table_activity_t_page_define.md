---
id: tbl_activity_t_page_define
object_type: Table
name: 开屏页定义表 (t_page_define)
aliases: [t_page_define, activity.t_page_define]
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

# 开屏页定义表 (t_page_define)

## 用途
物理表 `activity.t_page_define`,主键 `id`。开屏页定义表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `page_name` | varchar(128) | 页面名称 |
| `page_url` | varchar(255) | 页面地址 |
| `display_limit` | int | 展示最高次数 |
| `button_click_limit` | int | 点击按钮的最高次数 · 可空 |
| `product` | smallint | 1、cashnow，2、paylater，3、wecredit |
| `status` | smallint | 状态：1.生效2.失效 |
| `create_time` | timestamp | 待补 |
| `update_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `uk_name`:page_name (UNIQUE)
- `uk_url`:page_url (UNIQUE)
- `ix_t`:create_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

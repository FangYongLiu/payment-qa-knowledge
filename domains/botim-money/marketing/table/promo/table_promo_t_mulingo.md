---
id: tbl_promo_t_mulingo
object_type: Table
name: multi language message configuration (t_mulingo)
aliases: [t_mulingo, promo.t_mulingo]
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

# multi language message configuration (t_mulingo)

## 用途
物理表 `promo.t_mulingo`,主键 `id`。multi language message configuration。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | 待补 |
| `owner` | varchar(60) | 待补 |
| `name_space` | varchar(60) | 待补 |
| `msg_key` | varchar(200) | 待补 |
| `lang_key` | varchar(20) | 待补 |
| `version` | varchar(20) | 待补 |
| `msg_content` | varchar(2048) | 待补 |
| `memo` | varchar(200) | 待补 · 可空 |
| `create_at` | timestamp | 待补 |
| `update_at` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

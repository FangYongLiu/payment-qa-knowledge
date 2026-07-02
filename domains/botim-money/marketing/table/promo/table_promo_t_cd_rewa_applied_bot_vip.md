---
id: tbl_promo_t_cd_rewa_applied_bot_vip
object_type: Table
name: applied bot vip reward (t_cd_rewa_applied_bot_vip)
aliases: [t_cd_rewa_applied_bot_vip, promo.t_cd_rewa_applied_bot_vip]
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

# applied bot vip reward (t_cd_rewa_applied_bot_vip)

## 用途
物理表 `promo.t_cd_rewa_applied_bot_vip`,主键 `id`。applied bot vip reward。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `pname` | varchar(100) | the pname of the bot vip |
| `pid` | varchar(64) | the pid of the bot vip |
| `assign_status` | char(10) | Wait|Notified|Processing|Success|Failure · 可空 |
| `create_at` | timestamp | the create time of the bot_vip |
| `update_at` | timestamp | the update time of the bot_vip |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

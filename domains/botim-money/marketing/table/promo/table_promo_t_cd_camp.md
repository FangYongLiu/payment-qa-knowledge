---
id: tbl_promo_t_cd_camp
object_type: Table
name: campaign table (t_cd_camp)
aliases: [t_cd_camp, promo.t_cd_camp]
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

# campaign table (t_cd_camp)

## 用途
物理表 `promo.t_cd_camp`,主键 `id`。campaign table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `merchant_id` | char(32) | merchant id |
| `code` | varchar(20) | code of the campaign |
| `title` | varchar(128) | title of the campaign |
| `subtitle` | varchar(1024) | subtitle of the campaign |
| `description` | varchar(1024) | description of the campaign · 可空 |
| `detail_url` | varchar(1024) | detail url of the campaign |
| `scope` | varchar(15) | Scope: General|ApplyToServices |
| `start_at` | timestamp | start time of the campaign · 可空 |
| `end_at` | timestamp | end time of the campaign · 可空 |
| `max_audiences` | int | max audiences of the campaign |
| `joined_audiences` | int | joined audiences of the campaign |
| `status` | varchar(12) | Status: Preparing|Running|Paused|Terminated|Ended |
| `kind` | char(10) | Kind: General|Cycled|Referral|Cashback|BotMsg|AddUp|CheckOut|GameRefer |
| `create_at` | timestamp | create time |
| `update_at` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- `idx_merchant_code`:merchant_id, code

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

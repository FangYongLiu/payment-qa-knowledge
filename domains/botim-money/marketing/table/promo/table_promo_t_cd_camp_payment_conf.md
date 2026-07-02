---
id: tbl_promo_t_cd_camp_payment_conf
object_type: Table
name: campaign payment conf (t_cd_camp_payment_conf)
aliases: [t_cd_camp_payment_conf, promo.t_cd_camp_payment_conf]
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

# campaign payment conf (t_cd_camp_payment_conf)

## 用途
物理表 `promo.t_cd_camp_payment_conf`,主键 `id`。campaign payment conf。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | varchar(32) | ulid |
| `campaign_id` | varchar(32) | campaign id |
| `reward_service` | varchar(32) | reward service |
| `start_at` | timestamp | start at |
| `end_at` | timestamp | end at |
| `apply_count` | int | apply count |
| `total_apply_count` | int | total apply count |
| `product_code` | varchar(64) | product code |
| `merchant_ids` | varchar(255) | merchant ids |
| `short_no` | varchar(32) | short no |
| `method_type` | varchar(20) | method type |
| `channel` | varchar(20) | channel |
| `description` | varchar(255) | description |
| `status` | varchar(20) | status |
| `create_at` | timestamp | created at |
| `update_at` | timestamp | updated at |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

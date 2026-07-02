---
id: tbl_promo_t_cd_camp_cycle_conf
object_type: Table
name: camp cycle conf (t_cd_camp_cycle_conf)
aliases: [t_cd_camp_cycle_conf, promo.t_cd_camp_cycle_conf]
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

# camp cycle conf (t_cd_camp_cycle_conf)

## 用途
物理表 `promo.t_cd_camp_cycle_conf`,主键 `id`。camp cycle conf。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `merchant_id` | varchar(32) | merchant id |
| `campaign_id` | varchar(32) | campaign id |
| `source` | varchar(20) | message source from |
| `rule` | varchar(10) | enum: Daily|Weekly|Monthly|Once |
| `reward_max` | int | reward max in total |
| `start_at` | timestamp | create time |
| `end_at` | timestamp | create time |
| `status` | varchar(10) | Status: Preparing|Running|Paused|Terminated|Ended |
| `create_at` | timestamp | create time |
| `update_at` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

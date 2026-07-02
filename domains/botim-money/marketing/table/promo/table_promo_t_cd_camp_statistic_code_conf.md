---
id: tbl_promo_t_cd_camp_statistic_code_conf
object_type: Table
name: campaign statistic code conf (t_cd_camp_statistic_code_conf)
aliases: [t_cd_camp_statistic_code_conf, promo.t_cd_camp_statistic_code_conf]
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

# campaign statistic code conf (t_cd_camp_statistic_code_conf)

## 用途
物理表 `promo.t_cd_camp_statistic_code_conf`,主键 `id`。campaign statistic code conf。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `campaign_id` | varchar(32) | campaign id |
| `merchant_id` | varchar(32) | merchant id |
| `generation` | char(10) | generate type| Specified|Auto |
| `generation_rule` | varchar(1024) | generate rule |
| `start_at` | timestamp | start at |
| `end_at` | timestamp | end at |
| `apply_count` | int | apply count |
| `total_apply_count` | int | total apply count |
| `personalized` | varchar(1024) | personalized · 可空 |
| `off` | char | off |

## 主键 / 索引
- 主键:`id`
- `idx_promo_code_conf_camp_id`:campaign_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

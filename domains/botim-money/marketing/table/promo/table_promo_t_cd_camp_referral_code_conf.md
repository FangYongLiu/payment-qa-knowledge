---
id: tbl_promo_t_cd_camp_referral_code_conf
object_type: Table
name: t_cd_camp_referral_code_conf (t_cd_camp_referral_code_conf)
aliases: [t_cd_camp_referral_code_conf, promo.t_cd_camp_referral_code_conf]
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

# t_cd_camp_referral_code_conf (t_cd_camp_referral_code_conf)

## 用途
物理表 `promo.t_cd_camp_referral_code_conf`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `campaign_id` | char(32) | campaign id |
| `start_at` | timestamp | start time |
| `end_at` | timestamp | end time |
| `binding_limit` | int | binding limit |
| `apply_count` | int | apply count |
| `total_count` | int | total count |
| `target_url` | varchar(255) | target url |
| `share_url` | varchar(255) | share url |
| `off` | char | off |
| `personalized` | varchar(255) | personalized · 可空 |
| `create_at` | timestamp | create time |
| `update_at` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

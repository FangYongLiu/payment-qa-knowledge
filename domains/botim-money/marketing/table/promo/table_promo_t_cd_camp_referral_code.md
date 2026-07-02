---
id: tbl_promo_t_cd_camp_referral_code
object_type: Table
name: t_cd_camp_referral_code (t_cd_camp_referral_code)
aliases: [t_cd_camp_referral_code, promo.t_cd_camp_referral_code]
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

# t_cd_camp_referral_code (t_cd_camp_referral_code)

## 用途
物理表 `promo.t_cd_camp_referral_code`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `code` | varchar(18) | code |
| `mobile` | varchar(20) | mobile |
| `nick_name` | varchar(64) | nick name · 可空 |
| `customer_id` | char(32) | customer id |
| `customer_type` | varchar(15) | customer type|PromoUnique|PayByUnique|PlatformUnique |
| `level` | int | level |
| `create_at` | timestamp | create time |
| `update_at` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- `idx_code`:code (UNIQUE)
- `idx_cd_camp_referral_customer_id`:customer_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

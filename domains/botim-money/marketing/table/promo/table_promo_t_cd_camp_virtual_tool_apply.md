---
id: tbl_promo_t_cd_camp_virtual_tool_apply
object_type: Table
name: virtual tool apply records for v13 campaigns (t_cd_camp_virtual_tool_apply)
aliases: [t_cd_camp_virtual_tool_apply, promo.t_cd_camp_virtual_tool_apply]
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

# virtual tool apply records for v13 campaigns (t_cd_camp_virtual_tool_apply)

## 用途
物理表 `promo.t_cd_camp_virtual_tool_apply`,主键 `id`。virtual tool apply records for v13 campaigns。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `campaign_id` | varchar(32) | campaign id |
| `virtual_tool_conf_id` | varchar(32) | virtual tool conf id |
| `customer_id` | varchar(32) | customer id · 可空 |
| `customer_uid` | varchar(64) | customer uid · 可空 |
| `customer_payby_mid` | varchar(64) | customer payby mid · 可空 |
| `amount` | decimal(19, 4) | transaction amount |
| `create_at` | timestamp | created at |
| `update_at` | timestamp | updated at |

## 主键 / 索引
- 主键:`id`
- `idx_campaign_id`:campaign_id
- `idx_customer_id`:customer_id
- `idx_customer_uid`:customer_uid
- `idx_virtual_tool_apply_time`:create_at
- `idx_virtual_tool_conf_id`:virtual_tool_conf_id

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_promo_t_cd_rewa_applied_discount
object_type: Table
name: applied bot vip reward (t_cd_rewa_applied_discount)
aliases: [t_cd_rewa_applied_discount, promo.t_cd_rewa_applied_discount]
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

# applied bot vip reward (t_cd_rewa_applied_discount)

## 用途
物理表 `promo.t_cd_rewa_applied_discount`,主键 `id`。applied bot vip reward。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | ulid |
| `hit_calc_rule_id` | varchar(32) | the calc rule id |
| `calc_amount` | decimal(19, 4) | the calc rule amount of the discount |
| `calc_rule_name` | varchar(20) | the calc rule name of the discount |
| `calc_rule_json` | varchar(1024) | the calc rule json of the discount |
| `create_at` | timestamp | the create time of the discount |
| `update_at` | timestamp | the update time of the discount |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

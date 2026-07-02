---
id: tbl_botimsnpl_t_sl_coupon
object_type: Table
name: t_sl_coupon (t_sl_coupon)
aliases: [t_sl_coupon, botimsnpl.t_sl_coupon]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: botimsnpl schema DDL
tags: [lending, botimsnpl]
sensitivity: normal
related_services: []
---

# t_sl_coupon (t_sl_coupon)

## 用途
物理表 `botimsnpl.t_sl_coupon`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 · 可空 |
| `campaign_code` | varchar(50) | campaign code |
| `coupon_code` | varchar(50) | coupon code |
| `coupon_desc` | varchar(255) | coupon description |
| `coupon_type` | int(4) | coupon type, 0-interest discount, 1-cashback |
| `discount` | decimal(10, 2) | discount percentage, like 10%, will save 10 · 可空 |
| `discount_tip` | varchar(255) | discount tip · 可空 |
| `single_amount_limit` | decimal(10, 2) | single discount amount limit · 可空 |
| `total_amount_limit` | decimal(12, 2) | total discount amount limit · 可空 |
| `begin_time` | timestamp | begin time |
| `end_time` | timestamp | end time |
| `version` | int(4) | version · 可空 |
| `open_flag` | varchar(2) | flag: Y/N |
| `operator` | varchar(100) | operator |
| `ext` | varchar(255) | ext · 可空 |
| `created_time` | timestamp | created time |
| `last_modified` | timestamp | last modified time |

## 主键 / 索引
- 主键:`id`
- `idx_coupon_code_ver`:coupon_code, version
- `idx_coupon_created_time`:created_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

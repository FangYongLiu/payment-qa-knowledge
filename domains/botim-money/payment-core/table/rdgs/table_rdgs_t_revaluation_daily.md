---
id: tbl_rdgs_t_revaluation_daily
object_type: Table
name: 直连渠道每日估值信息 (t_revaluation_daily)
aliases: [t_revaluation_daily, rdgs.t_revaluation_daily]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: rdgs schema DDL
tags: [payment-core, rdgs]
sensitivity: normal
related_services: []
---

# 直连渠道每日估值信息 (t_revaluation_daily)

## 用途
物理表 `rdgs.t_revaluation_daily`,主键 `id`。直连渠道每日估值信息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键ID |
| `channel_code` | varchar(12) | 渠道CODE |
| `country_code` | char(2) | 国家CODE |
| `local_currency` | char(3) | 本币币种 |
| `foreign_currency` | char(3) | 外币币种 |
| `before_foreign_amount` | decimal(15, 4) | 期初外币金额 |
| `before_local_amount` | decimal(15, 4) | 期初本币金额 |
| `trade_foreign_amount` | decimal(15, 4) | 交易外币金额 |
| `trade_local_amount` | decimal(15, 4) | 交易金额;支付成功金额-退款金额 |
| `dealing_foreign_amount` | decimal(15, 4) | 换汇外币金额 |
| `dealing_local_amount` | decimal(15, 4) | 换汇本币金额 |
| `after_foreign_amount` | decimal(15, 4) | 期末外币金额 |
| `after_local_amount` | decimal(15, 4) | 期末本币金额 |
| `corridor_fee` | decimal(15, 4) | 外部渠道总费用 |
| `corridor_fee_currency` | char(3) | 外部渠道费用币种 |
| `local_revaluation_amount` | decimal(15, 4) | 总估值收益 |
| `local_margin_amount` | decimal(15, 4) | 汇差收益 · 可空 |
| `revaluation_rate` | decimal(15, 5) | 估值汇率 |
| `cumulative_margin` | decimal(15, 4) | 月累计利润 · 可空 |
| `revaluation_date` | datetime | 估值日期 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |
| `extension` | varchar(255) | 扩展参数 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_create_time`:create_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

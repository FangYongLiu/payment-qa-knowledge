---
id: tbl_scoupon_t_settle_config
object_type: Table
name: 结算配置表 (t_settle_config)
aliases: [t_settle_config, scoupon.t_settle_config]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: scoupon schema DDL
tags: [marketing, scoupon]
sensitivity: normal
related_services: []
---

# 结算配置表 (t_settle_config)

## 用途
物理表 `scoupon.t_settle_config`,主键 `id`。结算配置表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(17) | 主键 |
| `merchant_id` | varchar(32) | 商户ID |
| `settle_amount` | decimal(15, 4) | 结算金额 |
| `currency` | char(3) | 币种 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 修改时间 |
| `coupon_id` | bigint | 券ID |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

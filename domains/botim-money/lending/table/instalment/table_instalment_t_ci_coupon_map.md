---
id: tbl_instalment_t_ci_coupon_map
object_type: Table
name: 优惠卷映射表 (t_ci_coupon_map)
aliases: [t_ci_coupon_map, instalment.t_ci_coupon_map]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: instalment schema DDL
tags: [lending, instalment]
sensitivity: normal
related_services: []
---

# 优惠卷映射表 (t_ci_coupon_map)

## 用途
物理表 `instalment.t_ci_coupon_map`,主键 `id`。优惠卷映射表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int unsigned | 主健 · 可空 |
| `created_time` | timestamp | 创建时间 · 可空 |
| `last_modified` | timestamp | 修改时间 · 可空 |
| `status` | smallint(5) | 初始 0 , 冻结 1, 核销 2，使用失败 -1 |
| `discounted_price` | decimal(15, 2) | 抵扣金额 · 可空 |
| `coupon_id` | varchar(64) | 优惠券ID |
| `order_no` | varchar(50) | 订单号 |
| `ctype` | smallint(5) | 优惠类型：0 手续费 1 本金 2 罚息 |
| `event_id` | varchar(200) | 事件ID · 可空 |
| `origin_price` | decimal(15, 2) | 原始金额 · 可空 |
| `user_id` | varchar(50) | 用户ID · 可空 |
| `request_no` | varchar(64) | 请求流水 · 可空 |
| `coupon_fee` | decimal(15, 2) | 优惠卷面值 折扣卷1=1% · 可空 |
| `coupon_type` | tinyint(5) | 优惠卷类型 1立减 2折扣 |
| `member_id` | varchar(20) | 优惠持有人 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_coupon_id`:coupon_id
- `idx_member_id`:member_id
- `idx_order_no`:order_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

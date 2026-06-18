---
id: tbl_acquireii_t_promotion_info
object_type: Table
domain: pos-business
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_promotion_info.md
tags:
- promotion
- coupon
- discount
subdomain: acquireii
module: null
sensitivity: normal
name: 优惠券信息表 t_promotion_info
aliases:
- acquireii.t_promotion_info
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
记录一笔订单使用的**促销活动 / 优惠券信息**，包括优惠类型、优惠金额及对应订单关联。

典型场景：
- 用户使用优惠券支付（如满 100 减 20）
- 平台活动优惠（如新用户首单减免）
- 积分抵扣

表名：`acquireii.t_promotion_info`，主键 `id`，重要程度 ⭐⭐⭐。

## 关键列

**主键和关联**
- `id` bigint ✅ 主键
- `global_id` bigint ✅ 对应订单 global_id

**优惠券信息**
- `promotion_id` varchar(64) ✅ 促销活动 ID
- `promotion_type` varchar(32) 促销类型（COUPON / DISCOUNT / POINTS 等）
- `promotion_name` varchar(200) 促销活动名

**优惠金额**
- `discount_amount` decimal(19,4) 优惠金额
- `discount_currency` varchar(50) 优惠金额币种

**时间**
- `created_time` timestamp(3) ✅ 创建时间

## 主键/索引
| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | id | 主键 |
| `i_pi_gi` | global_id | 通过订单查优惠 |
| `i_pi_pid` | promotion_id | 按活动查 |

关联表：`t_acquire_order`（N:1，关联字段 `global_id`）。

## 校验点(QA 关注)
1. **一笔订单可有多个优惠**：SUM 统计时不要漏算
2. **优惠金额不一定等于实际抵扣**：部分优惠有上限
3. **退款时是否退优惠**：业务上需明确（通常不退）
4. 校验 `global_id` 与 `t_acquire_order` 的对应关系
5. 校验 `discount_amount` 与 `discount_currency` 的一致性，避免币种缺失
6. `promotion_type` 取值需符合枚举（COUPON / DISCOUNT / POINTS 等）

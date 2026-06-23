---
id: tbl_acquireii_t_promotion_info
object_type: Table
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
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
related_services:
- svc_acquireii
---

## 用途

`acquireii.t_promotion_info`（优惠券信息表）记录一笔订单使用的**促销活动 / 优惠券信息**，包括优惠类型、优惠金额及对应订单关联，是收单订单交易明细的子表之一。重要程度 ⭐⭐⭐，主键 `id`。

典型场景：
- 用户使用优惠券支付（如满 100 减 20）
- 平台活动优惠（如新用户首单减免）
- 积分抵扣

## 在交易链路中的位置

下单/支付阶段，若订单携带优惠信息，则在主订单 `t_acquire_order` 落库的同时，按优惠条目写入 `t_promotion_info`（一笔订单可对应多条优惠记录）。它与 `t_goods_detail`（商品明细）、`t_amount_detail`（金额明细）、`t_payment_info`（支付信息）共同构成订单的完整业务快照：

- `t_acquire_order` (1) ──< `t_promotion_info` (N)，通过 `global_id` 关联
- `t_amount_detail` 记录订单金额构成（订单总额、应付额等），`t_promotion_info` 解释其中优惠抵扣的来源
- 退款时查看 `t_refund_order`，业务上是否回退优惠通常需单独约定

## 关键列

**主键和关联**
- `id` bigint ✅ 主键
- `global_id` bigint ✅ 对应订单 `t_acquire_order.global_id`

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

## 关联表

| 关联表 | 关系 | 关联字段 | 说明 |
|--------|------|---------|------|
| `t_acquire_order` | N:1 | `global_id` | 优惠归属的收单订单主表 |
| `t_amount_detail` | 同订单 | `global_id` | 订单金额构成，与优惠金额需对账 |
| `t_goods_detail` | 同订单 | `global_id` | 商品明细，部分优惠按商品维度发放 |
| `t_payment_info` | 同订单 | `global_id` | 实际支付信息，实付 = 应付 - 优惠抵扣 |
| `t_refund_order` | 同订单 | `global_id` | 退款时是否退优惠的业务校验依据 |

## QA 落库检查要点

1. **多条优惠合并**：一笔订单可有多个优惠，按 `global_id` 聚合 SUM 统计时不要漏算/重算。
2. **优惠金额 ≠ 实际抵扣**：部分优惠有上限或封顶，需结合 `t_amount_detail` 校验最终抵扣是否一致。
3. **退款是否退优惠**：业务上需明确（通常不退），核对 `t_refund_order` 与本表的金额关系。
4. **外键一致性**：校验 `global_id` 在 `t_acquire_order` 中存在且状态正确。
5. **金额-币种一致性**：`discount_amount` 非空时 `discount_currency` 必须存在，且币种应与订单币种一致。
6. **枚举值校验**：`promotion_type` 取值需符合枚举（COUPON / DISCOUNT / POINTS 等）。
7. **必填字段**：`id`、`global_id`、`promotion_id`、`created_time` 必须落库。
8. **时间合理性**：`created_time` 应与 `t_acquire_order` 的下单时间接近，不早于订单创建时间。
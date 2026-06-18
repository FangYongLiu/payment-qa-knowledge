---
id: tbl_acquireii_t_amount_detail
object_type: Table
domain: pos-business
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_amount_detail.md
tags:
- 金额
- 小费
- VAT
- 折扣
subdomain: order
module: amount
sensitivity: normal
name: 金额明细表
aliases:
- t_amount_detail
- acquireii.t_amount_detail
related_services: []
related_tables:
- tbl_acquireii_t_acquire_order
- tbl_acquireii_t_dcc_info
- tbl_acquireii_t_goods_detail
- tbl_acquireii_t_payment_info
- tbl_acquireii_t_promotion_info
related_scenarios:
- scn_acquire_product_apply
- scn_merchant_transaction_db_check
- scn_payment_code_scanned_by_pos
- scn_payment_code_scanned_by_scanner
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

`t_amount_detail`(金额明细表) 记录一笔收单订单**金额的详细构成**:净额(net_amount)、小费(tip)、VAT 税额、可折扣金额(discountable_amount)。

订单总金额组成公式:

```
total_amount ≈ net_amount(amount) + tip_amount + vat_amount - discount
```

典型业务场景:
- 餐厅小费(tip)
- 商品打折(discount)
- VAT 税单独标注(阿联酋本地业务税务合规,VAT 通常 5%)
- 出租车等需小费业务

## 在交易链路中的位置

该表属于收单交易**订单维度的辅助明细**,与订单主表 1:1 关联:

```
t_acquire_order (订单主表, global_id 主键)
    ├── t_amount_detail        ← 金额拆分明细 (本表, 1:1, 可选)
    ├── t_payment_info         ← 支付通道/卡/渠道结果
    ├── t_promotion_info       ← 优惠券/折扣明细
    ├── t_goods_detail         ← 商品明细
    └── t_dcc_info             ← DCC 币种转换信息
```

订单创建时,如果业务侧上送了 tip / vat / discountable 等字段,即与主订单一同写入本表;若是简单订单,本表可能无对应记录。

## 与关联表的关系

| 关联表 | 关系 | 说明 |
|--------|------|------|
| `t_acquire_order` | 1:1,通过 `global_id` | 主表,提供 total_amount、currency、create_time 等。本表无时间字段,时间需 JOIN 主表获得 |
| `t_promotion_info` | 间接 | 折扣/优惠券明细,与本表 `discountable_amount` 概念配合 |
| `t_payment_info` | 间接 | 实际支付流水/支付渠道结果 |
| `t_goods_detail` | 间接 | 商品维度的金额可与本表合计金额对账 |
| `t_dcc_info` | 间接 | 若发生 DCC,需结合 DCC 后币种与金额一起核对 |

## 关键列

| 字段 | 类型 | 说明 |
|------|------|------|
| `global_id` | bigint | 主键,对应订单 global_id |
| `amount` | decimal(19,4) | 净额(net_amount) |
| `currency_code` | varchar(50) | 净额币种 |
| `discountable_amount` | decimal(19,4) | 可折扣金额 |
| `discountable_currency_code` | varchar(50) | 可折扣金额币种 |
| `tip_amount` | decimal(19,4) | 小费金额 |
| `tip_currency_code` | varchar(50) | 小费币种 |
| `vat_amount` | decimal(19,4) | VAT 税额 |
| `vat_currency_code` | varchar(50) | VAT 税币种 |

## 主键 / 索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | global_id | 主键(同时充当与订单主表的关联键) |

## QA 落库检查要点

1. **无时间字段**:本表不存储任何时间列,时间过滤一律走 `t_acquire_order.create_time` / `gmt_create`。
2. **可选记录,使用 LEFT JOIN**:并非所有订单都有金额明细,简单订单可能没数据,查询时务必 `LEFT JOIN t_amount_detail USING(global_id)`,避免主订单被过滤丢失。
3. **金额计算一致性**:校验 `o.total_amount ≈ a.amount + a.tip_amount + a.vat_amount`(并在有折扣时减去 discount),差值应为 0。
4. **小费场景特殊**:`tip_amount` 主要出现在餐厅、出租车等业务,其他场景应为 0 或 NULL。
5. **币种一致性**:`currency_code`、`tip_currency_code`、`vat_currency_code`、`discountable_currency_code` 通常应与订单主币种一致,不一致需警惕(可能是 DCC 或脏数据,需结合 `t_dcc_info` 核对)。
6. **VAT 5% 合规校验(阿联酋)**:可做 `vat_amount / amount ≈ 5%` 的近似检查。
7. **写入时机**:本表应在订单创建时与主表一并写入;若主表已存在而本表缺失且业务上送了 tip/vat/discountable,需排查写入逻辑。
8. **金额精度**:decimal(19,4),比较金额时注意四舍五入与精度差异(建议用容差 `< 0.01`)。

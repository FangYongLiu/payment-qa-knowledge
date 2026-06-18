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
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

记录一笔订单**金额的详细构成**：净额（net_amount）、小费（tip）、VAT 税、可折扣金额（discountable_amount）。订单总金额由多个部分组成：净额 + 小费 + 税 - 折扣。

典型场景：
- 餐厅小费（tip）
- 商品打折（discount）
- VAT 税单独标注
- 阿联酋本地业务税务合规

与 `t_acquire_order` 1:1 关联，关联字段 `global_id`。订单创建时一起写入。

## 关键列

| 字段 | 类型 | 说明 |
|------|------|------|
| `global_id` | bigint | 主键，对应订单 global_id |
| `amount` | decimal(19,4) | 净额（net_amount） |
| `currency_code` | varchar(50) | 净额币种 |
| `discountable_amount` | decimal(19,4) | 可折扣金额 |
| `discountable_currency_code` | varchar(50) | 可折扣金额币种 |
| `tip_amount` | decimal(19,4) | 小费金额 |
| `tip_currency_code` | varchar(50) | 小费币种 |
| `vat_amount` | decimal(19,4) | VAT 税额 |
| `vat_currency_code` | varchar(50) | VAT 税币种 |

## 主键/索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | global_id | 主键 |

## 校验点(QA 关注)

1. **没有时间字段**：本表无时间列，时间需通过 `t_acquire_order` 获取。
2. **不是所有订单都有明细**：简单订单 `t_amount_detail` 可能没数据，查询使用 LEFT JOIN。
3. **金额计算一致性**：校验 `o.total_amount` ≈ `a.amount + a.tip_amount + a.vat_amount`，差值应为 0（或减去折扣后为 0）。
4. **小费场景特殊**：`tip_amount` 主要出现在餐厅、出租车类业务。
5. **币种应一致**：`currency_code`、`tip_currency_code`、`vat_currency_code`、`discountable_currency_code` 通常应为同一币种，不一致时需警惕。
6. **VAT 是 5%**（阿联酋）：可作 `vat_amount / amount ≈ 5%` 的合规性验证。

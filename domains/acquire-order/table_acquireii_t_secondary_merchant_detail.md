---
id: tbl_acquireii_t_secondary_merchant_detail
object_type: Table
domain: acquire-order
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_secondary_merchant_detail.md
tags:
- 二级商户
- 聚合支付
- MCC
subdomain: null
module: null
sensitivity: normal
name: 二级商户明细表
aliases:
- t_secondary_merchant_detail
- acquireii.t_secondary_merchant_detail
related_services: []
related_tables:
- tbl_acquireii_t_acquire_order
- tbl_acquireii_t_amount_detail
- tbl_acquireii_t_goods_detail
- tbl_acquireii_t_payment_info
- tbl_acquireii_t_sharing_info
- tbl_acquireii_t_terminal_detail
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
`acquireii.t_secondary_merchant_detail` 记录订单中的**二级商户信息**，主要服务于聚合支付、SaaS 平台等多商户接入场景。

- **一级商户（partner / partner_id）**：直接和支付公司签约的商户，主体见 `t_acquire_order.partner_id`。
- **二级商户（merchant / merchant_id）**：通过一级商户接入的下游商户（如平台上的店铺、加盟商）。

该表与 `t_acquire_order` **1:1 关联**（通过 `global_id`），仅在聚合支付/SaaS 类订单中落库；普通直连商户订单本表为空。

## 在交易链路中的位置

```
t_acquire_order (主单, partner_id=一级商户)
  ├── t_secondary_merchant_detail  ← 本表 (merchant_id=二级商户)
  ├── t_payment_info               (支付信息)
  ├── t_amount_detail              (金额/手续费明细，费率受 MCC 影响)
  ├── t_terminal_detail            (终端信息)
  ├── t_goods_detail               (商品明细)
  └── t_sharing_info               (分账信息，常与二级商户配合使用)
```

收单引擎在受理订单时，若识别为聚合支付（如付款码被扫、SaaS 平台代下单），会将下游店铺信息落入本表，供清算、分账、风控、费率计算引用。

## 关键列

| 字段 | 类型 | 说明 |
|------|------|------|
| `global_id` | bigint | 主键，对应 `t_acquire_order.global_id` |
| `mcc` | varchar(32) | MCC（商户类别码），影响费率与风控 |
| `name` | varchar(255) | 二级商户名 |
| `merchant_id` | varchar(64) | 二级商户业务 ID（外部标识） |
| `merchant_inner_id` | bigint | 二级商户内部 ID |

## 主键 / 索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | global_id | 主键，与订单 1:1 |
| `idx_smd_id` | merchant_id | 按二级商户业务 ID 查询 |

## 与关联表的关系

| 关联表 | 关系 | 关联键 | 说明 |
|--------|------|--------|------|
| `t_acquire_order` | 1:1 | `global_id` | 主单，提供 partner_id（一级商户） |
| `t_amount_detail` | 通过订单 | `global_id` | 费率计算依赖本表 mcc |
| `t_sharing_info` | 通过订单 | `global_id` | 分账目标常为二级商户 |
| `t_payment_info` | 通过订单 | `global_id` | 支付明细 |
| `t_terminal_detail` | 通过订单 | `global_id` | 受理终端归属二级商户 |

## 校验点（QA 落库关注）

1. **订单类型区分**：聚合支付/SaaS 订单本表必须有记录；普通直连订单本表应为空，避免误判。
2. **一二级商户区分**：`partner_id`（来自 `t_acquire_order`）= 一级商户，`merchant_id`（本表）= 二级商户，**严禁混用**；用例断言时分别取值校验。
3. **MCC 影响费率**：不同 MCC 类目对应不同手续费费率，校验 `t_amount_detail` 中费率/手续费金额时需结合本表 `mcc` 计算。
4. **MCC 风控覆盖**：高风险 MCC（如赌博、成人）会触发严格风控，需覆盖此类用例并校验风控决策。
5. **1:1 一致性**：`global_id` 必须与 `t_acquire_order.global_id` 一一对应，不允许孤儿记录或重复。
6. **二级商户 ID 一致性**：`merchant_id` 与 `merchant_inner_id` 应能在商户档案系统对得上；`name` 与档案保持一致。
7. **分账场景联动**：若订单存在 `t_sharing_info`，分账接收方通常应为本表中的二级商户，需做交叉校验。

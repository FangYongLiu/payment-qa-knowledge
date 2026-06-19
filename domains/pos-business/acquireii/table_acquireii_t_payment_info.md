---
id: tbl_acquireii_t_payment_info
object_type: Table
domain: device-pos
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_payment_info.md
tags:
- 收单
- 支付
- 结算
- 手续费
subdomain: acquireii
module: null
sensitivity: normal
name: 支付信息表 (t_payment_info)
aliases:
- acquireii.t_payment_info
related_services: []
related_tables:
- tbl_acquireii_t_acquire_order
- tbl_acquireii_t_amount_detail
- tbl_acquireii_t_card_info
- tbl_acquireii_t_channel_param
- tbl_acquireii_t_dcc_info
- tbl_acquireii_t_preauth_relation
- tbl_acquireii_t_promotion_info
- tbl_acquireii_t_refund_order
- tbl_acquireii_t_stmt_event
related_scenarios:
- scn_acquire_product_apply
- scn_cko_subscription_test_cards
- scn_merchant_transaction_db_check
- scn_mit_autodebit
- scn_mit_cit_directpay_first
- scn_mit_cit_directpay_subsequent
- scn_mit_cit_payandsign
- scn_payment_code_scanned_by_pos
- scn_payment_code_scanned_by_scanner
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

`acquireii.t_payment_info` 记录订单**支付完成后**的详细信息（实际收款金额、手续费、税费、结算等），是收单交易链路中「钱已经动了」之后的核心落库表。表注释：收单数据。

它与订单主表 `t_acquire_order` 通过 `global_id` 一一对应，但**生命周期不同**：

- 订单刚创建（CREATED/PROCESSING）→ 本表**无数据**
- 支付成功（PAID/SUCCESS）→ 写入本表（`paid_time`、`paid_amount` 等）
- 结算完成（T+1 / T+N）→ 更新 `settled_time`、`settlement_amount`、`settlement_currency_code`

## 在交易链路中的位置

```
t_acquire_order (订单创建,声明金额 total_amount)
      │ global_id 1:1
      ▼
t_payment_info (支付成功后写入,实际 paid_amount;结算后回填 settled_*)
      │
      ├── t_card_info        (1:1, global_id, 卡相关支付才有)
      ├── t_channel_param    (N:1, channel_param_id, 渠道配置)
      ├── t_dcc_info         (1:1, global_id, DCC 场景才有)
      ├── t_amount_detail    (金额明细拆分)
      ├── t_promotion_info   (优惠/抵扣)
      └── t_stmt_event       (对账事件,与结算字段勾稽)
```

## 关键列

### 主键与支付信息
- `global_id` (bigint, ✅ 主键)：对应 `t_acquire_order.global_id`
- `paid_time` (timestamp(3))：支付成功时间
- `pay_channel` (varchar(200))：支付渠道
- `payer_mid` (varchar(200))：付款人 mid

### 支付金额
- `paid_currency_code` (varchar(50))：收单币种
- `paid_amount` (decimal(19,4))：收单金额（实际支付金额）

### 商户手续费
- `payer_fee_currency_code` / `payer_fee_amount`：付款方手续费币种 / 金额（用户承担）
- `payee_fee_currency_code` / `payee_fee_amount`：收款方手续费币种 / 金额（商户承担）

### 含税 / 不含税（VAT 拆分）
- `pfbt_amt` (decimal(19,4))：不含税金额（payee_fee_before_tax）
- `pfbt_crcy` (varchar(16))：不含税金额币种
- `pf_vat` (decimal(19,4))：VAT 税额
- `pfv_crcy` (varchar(16))：VAT 税币种

### 结算
- `settlement_currency_code` (varchar(50))：结算币种
- `settlement_amount` (decimal(19,4))：结算金额
- `settled_time` (timestamp(3))：结算时间

### 其他
- `channel_param_id` (bigint)：渠道参数 ID，关联 `t_channel_param`
- `extension_info` (varchar(512))：扩展信息
- `created_time` / `last_updated_time` (timestamp(3))
- `data_version` (bigint)：数据版本（乐观锁）

## 主键 / 索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | `global_id` | 主键，唯一对应一笔订单 |
| `i_ao_pt` | `paid_time` | 按支付时间检索 |
| `i_ao_st` | `settled_time` | 按结算时间检索 / 对账 |

## 关联表

| 关联表 | 关系 | 关联字段 | 说明 |
|--------|------|----------|------|
| `t_acquire_order` | 1:1 | `global_id` | 订单主表，先有它才能有本表 |
| `t_card_info` | 1:1 | `global_id` | 卡支付场景的卡信息 |
| `t_channel_param` | N:1 | `channel_param_id` | 支付渠道配置 |
| `t_dcc_info` | 1:1 | `global_id` | DCC 场景下的汇率/原币信息 |
| `t_amount_detail` | 1:N | `global_id` | 金额明细拆分 |
| `t_promotion_info` | 1:N | `global_id` | 优惠券抵扣信息 |
| `t_stmt_event` | 1:N | `global_id` | 对账事件，用于核对结算 |
| `t_preauth_relation` | — | `global_id` | 预授权场景下的关联 |

## QA 落库检查要点

1. **未支付订单查不到数据**：本表只在支付成功后写入，测试 CREATED / PROCESSING / FAILED 等状态时不应在此表查到记录。仅 `t_acquire_order` 有行。
2. **paid_amount vs total_amount**：
   - `t_acquire_order.total_amount`：订单声明金额
   - `t_payment_info.paid_amount`：实际支付金额
   - 通常相等；**DCC 场景可能不同**（需结合 `t_dcc_info` 校验原币/换算币）。
3. **手续费两个方向都要查**：
   - `payer_fee_amount` / `payer_fee_currency_code` —— 用户承担
   - `payee_fee_amount` / `payee_fee_currency_code` —— 商户承担
   - 分别校验金额与币种正确入账，不要混淆方向。
4. **结算时间与支付时间分离**：
   - `paid_time` 在支付成功瞬间写入
   - `settled_time` 通常 T+1 或 T+N，未结算时为空；结算后回填，并配套写入 `settlement_amount` / `settlement_currency_code`
   - 对账场景需联动 `t_stmt_event` 校验。
5. **VAT 税单独记录（阿联酋等市场 5% VAT）**：
   - `pfbt_amt` + `pf_vat` 与 `payee_fee_amount` 之间的勾稽关系必须成立
   - 币种字段 `pfbt_crcy` / `pfv_crcy` 不能缺失，且应与对应金额币种一致。
6. **币种字段一致性**：`paid_currency_code`、`payer_fee_currency_code`、`payee_fee_currency_code`、`settlement_currency_code` 各自独立。跨币种结算 / DCC / VAM 多币种场景需分别校验，不能默认相等。
7. **关联完整性**：
   - `global_id` 必须能在 `t_acquire_order` 找到
   - 卡支付场景下 `t_card_info` 应同步存在
   - `channel_param_id` 必须能在 `t_channel_param` 中查到
   - 不应出现孤儿记录。
8. **MIT/CIT、订阅、AutoDebit 场景**：每次实际扣款都会生成一条新的 `t_acquire_order` + `t_payment_info`；签约本身（PayAndSign 的签约部分、首次 CIT）若无实际扣款则不会落本表，需注意区分。
9. **预授权场景**：预授权请求阶段不一定写入；请款（capture）成功后才落 `t_payment_info`，可结合 `t_preauth_relation` 串联。

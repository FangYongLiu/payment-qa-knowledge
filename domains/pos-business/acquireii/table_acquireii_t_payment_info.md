---
id: tbl_acquireii_t_payment_info
object_type: Table
domain: pos-business
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
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

`acquireii.t_payment_info` 记录订单**支付完成后**的详细信息（金额、手续费、结算）。与 `t_acquire_order` 通过 `global_id` 一一对应：

- 订单刚创建 → 本表**无数据**
- 支付完成 → 写入本表
- 结算完成 → 更新 `settled_time`

表注释：收单数据。

## 关键列

### 主键与支付信息
- `global_id` (bigint, ✅ 主键)：对应 `t_acquire_order.global_id`
- `paid_time` (timestamp(3))：支付成功时间
- `pay_channel` (varchar(200))：支付渠道
- `payer_mid` (varchar(200))：付款人 mid

### 支付金额
- `paid_currency_code` (varchar(50))：收单币种
- `paid_amount` (decimal(19,4))：收单金额

### 商户手续费
- `payer_fee_currency_code` / `payer_fee_amount`：付款方手续费币种 / 金额
- `payee_fee_currency_code` / `payee_fee_amount`：收款方手续费币种 / 金额

### 含税 / 不含税
- `pfbt_amt` (decimal(19,4))：不含税金额（payee_fee_before_tax）
- `pfbt_crcy` (varchar(16))：不含税金额币种
- `pf_vat` (decimal(19,4))：VAT 税
- `pfv_crcy` (varchar(16))：VAT 税币种

### 结算
- `settlement_currency_code` (varchar(50))：结算币种
- `settlement_amount` (decimal(19,4))：结算金额
- `settled_time` (timestamp(3))：结算时间

### 其他
- `channel_param_id` (bigint)：渠道参数 ID
- `extension_info` (varchar(512))：扩展信息
- `created_time` / `last_updated_time` (timestamp(3))
- `data_version` (bigint)：数据版本

## 主键/索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | `global_id` | 主键 |
| `i_ao_pt` | `paid_time` | 按支付时间查 |
| `i_ao_st` | `settled_time` | 按结算时间查 |

关联表：
- `t_acquire_order` 1:1，关联字段 `global_id`
- `t_channel_param` N:1，关联字段 `channel_param_id`
- `t_card_info` 1:1，关联字段 `global_id`

## 校验点(QA 关注)

1. **未支付订单查不到数据**：本表只在支付成功后才有，测试未支付/支付中订单时不应在此表查到记录。
2. **paid_amount vs total_amount**：
   - `t_acquire_order.total_amount` 是订单声明金额
   - `t_payment_info.paid_amount` 是实际支付金额
   - 通常相等，**DCC 场景可能不同**，需要单独验证。
3. **手续费两个方向**：
   - `payer_fee_amount` —— 用户承担
   - `payee_fee_amount` —— 商户承担
   - 校验金额、币种是否分别正确入账。
4. **结算时间与支付时间分离**：`settled_time` 通常 T+1 或 T+N，未结算时 `settled_time` 应为空；结算后才回填。
5. **VAT 税单独记录**：阿联酋市场 5% VAT 必须分开，校验 `pfbt_amt` + `pf_vat` 与 `payee_fee_amount` 的勾稽关系，币种字段 `pfbt_crcy` / `pfv_crcy` 不能缺失。
6. **币种字段一致性**：`paid_currency_code`、`payer_fee_currency_code`、`payee_fee_currency_code`、`settlement_currency_code` 各自独立，跨币种结算场景需分别校验。
7. **关联完整性**：通过 `global_id` 与 `t_acquire_order`、`t_card_info` 一一对应，不应出现孤儿记录；`channel_param_id` 应在 `t_channel_param` 中存在。

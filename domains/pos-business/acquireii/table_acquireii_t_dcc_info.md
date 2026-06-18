---
id: tbl_acquireii_t_dcc_info
object_type: Table
domain: pos-business
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_dcc_info.md
tags:
- DCC
- 汇率
- 退款
subdomain: acquireii
module: dcc
sensitivity: normal
name: DCC信息表 t_dcc_info
aliases:
- t_dcc_info
- acquireii.t_dcc_info
related_services: []
related_tables:
- tbl_acquireii_t_acquire_order
- tbl_acquireii_t_amount_detail
- tbl_acquireii_t_dcc_info_log
- tbl_acquireii_t_payment_info
- tbl_acquireii_t_refund_order
related_scenarios:
- scn_acquire_product_apply
- scn_merchant_transaction_db_check
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

`acquireii.t_dcc_info` 记录一笔订单的 **DCC（Dynamic Currency Conversion，动态货币转换）信息**，包含汇率、加点、回扣等核心数据。当持卡人用本国货币结算非本国货币订单时，由收单方提供实时汇率转换并锁定汇率。

重要程度：⭐⭐⭐⭐⭐（DCC 是 Bug 高发区，尤其是退款汇率一致性问题）

典型场景：
- 外国游客在阿联酋用美元卡支付迪拉姆订单
- 收单系统提示 "用 USD 还是 AED 结算？"
- 用户选择 USD（DCC）→ 锁定当时汇率
- **退款时必须使用原订单汇率冲正**（常见 Bug 点）

## 在交易链路中的位置

```
[用户付款选择币种]
        │
        ▼
[t_acquire_order] ── 1:1 ──▶ [t_dcc_info]  (PURCHASE, 锁定汇率)
        │                          │
        │                          └─▶ [t_dcc_info_log] (历次询价/报价流水, 1:N)
        ▼
[t_refund_order] ── 1:1 ──▶ [t_dcc_info]  (REFUND, 必须复用原汇率)
```

该表挂在订单主键 `global_id` 上，是收单订单在 "币种与汇率" 维度的扩展信息，与金额明细 `t_amount_detail`、支付信息 `t_payment_info` 一起完整描述一笔订单的资金面。

## 关键列

### 主键和币种
- `global_id` (bigint, ✅ PK) —— 主键，对应订单 `global_id`
- `order_currency` (char(3)) —— 订单原币种（如 AED）
- `dcc_amount_cur` (char(3)) —— DCC 金额币种（如 USD）
- `dcc_amount` (decimal(19,4)) —— DCC 金额（转换后）

### 汇率核心
- `exchange_rate` (decimal(16,8)) —— **汇率**（当时锁定）
- `markup_rate` (decimal(16,8)) —— **加点率**（收单方加点，手续费的一部分）
- `rebate_rate` (decimal(16,8)) —— **回扣率**（返还给商户的比例）
- `rebate_amount` (decimal(19,4)) —— 回扣金额
- `rebate_amount_cur` (char(3)) —— 回扣币种

### 业务标识
- `dcc_quote_id` (varchar(64)) —— DCC 报价 ID（来自第三方汇率源，有效期通常 24h）
- `dcc_uptake` (varchar(20)) —— DCC 选择标志（用户是否接受 DCC）
- `trans_date` (timestamp(3)) —— 交易日期
- `partner_id` (varchar(64), ✅) —— 商户 ID
- `fund_type` (varchar(8)) —— **PURCHASE / REFUND**
- `status` (varchar(10)) —— 状态

### 时间和版本
- `created_time` (timestamp(3), ✅)
- `last_updated_time` (timestamp(3), ✅)
- `data_version` (bigint, ✅)

## 主键 / 索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | `global_id` | 主键 |
| `i_di_ct` | `created_time` | 按时间查 |
| `i_di_td_du` | `(trans_date, dcc_uptake)` | 常用：按交易日 + DCC 接受状态查 |

## 关联表

| 关联表 | 关系 | 关联键 | 说明 |
|--------|------|--------|------|
| `t_acquire_order` | 1:1 | `global_id` | 原始收单订单，`fund_type=PURCHASE` 的 DCC 行 |
| `t_refund_order` | 1:1 | `global_id` | 退款订单，对应 `fund_type=REFUND` 的 DCC 行，须复用原 rate |
| `t_dcc_info_log` | 1:N | `partner_id + dcc_quote_id` | 同一报价的询价/选择流水 |
| `t_payment_info` | 1:1 | `global_id` | 渠道支付信息，DCC 实际入账币种与渠道一致性参考 |
| `t_amount_detail` | 1:N | `global_id` | 金额明细，可与 `dcc_amount` 交叉校验 |

## QA 校验点（落库检查）

DCC 业务是 Bug 高发区，重点关注：

1. **退款汇率必须用原订单汇率**（最常见 Bug）
   - ❌ 退款时调取当时实时汇率
   - ✅ 退款时从原订单 `t_dcc_info` 读 `exchange_rate`
   - 校验 SQL：JOIN 退款记录与原订单的 `t_dcc_info`（`fund_type='REFUND'` vs `fund_type='PURCHASE'`），比对 `exchange_rate` 是否一致，不一致即 MISMATCH。

2. **fund_type 区分用途**：
   - `PURCHASE` —— 原订单 DCC 信息
   - `REFUND` —— 退款时新生成的 DCC 信息（应复用原 rate）

3. **dcc_uptake 是关键状态**：
   - 用户接受 DCC → 走 DCC 流程，`t_dcc_info` 有完整数据
   - 用户不接受 DCC → 走原币种结算，可能没数据或数据为 0

4. **markup_rate 合规**：加点率不能过高（合规要求），不同币种对、不同商户费率不同。

5. **rebate_rate 商户返点**：是商户接入 DCC 的主要动力，鼓励商户引导用户选择 DCC；`rebate_amount_cur` 与 `rebate_amount` 需匹配。

6. **dcc_quote_id 来自第三方汇率源**：有效期通常 24h，过期需要重新询价；可与 `t_dcc_info_log` 关联查报价历史。

7. **同币种不应该有 DCC**：若 `order_currency == dcc_amount_cur`，说明数据异常。

8. **金额一致性**：`dcc_amount` 应约等于 `order_amount * exchange_rate`（在 `t_acquire_order` / `t_amount_detail` 中取原币金额），允许精度误差。

9. **partner_id 与订单一致**：`t_dcc_info.partner_id` 必须与对应 `t_acquire_order.partner_id` 一致。

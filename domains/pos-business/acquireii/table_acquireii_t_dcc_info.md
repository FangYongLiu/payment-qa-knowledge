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
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

记录一笔订单的 **DCC（Dynamic Currency Conversion，动态货币转换）信息**，包含汇率、加点、回扣等核心数据。当用户用本国货币结算非本国货币订单时，由收单方提供实时汇率转换并锁定汇率。

典型场景：
- 外国游客在阿联酋用美元卡支付迪拉姆订单
- 收单系统提示"用 USD 还是 AED 结算？"
- 用户选择 USD（DCC）→ 锁定当时汇率
- **退款时必须使用原订单汇率冲正**（常见 Bug 点）

表名：`acquireii.t_dcc_info`，重要程度 ⭐⭐⭐⭐⭐。

## 关键列

### 主键和币种
- `global_id` (bigint, ✅) —— 主键，对应订单 global_id
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

## 主键/索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | `global_id` | 主键 |
| `i_di_ct` | `created_time` | 按时间查 |
| `i_di_td_du` | `(trans_date, dcc_uptake)` | 常用：按交易日 + DCC 接受状态查 |

关联表：
- `t_acquire_order` 1:1，关联 `global_id`
- `t_refund_order` 1:1（退款时），关联 `global_id`
- `t_dcc_info_log` 1:N，关联 `partner_id + dcc_quote_id`

## 校验点(QA 关注)

DCC 业务是 Bug 高发区，重点关注：

1. **退款汇率必须用原订单汇率**（最常见 Bug）
   - ❌ 退款时调取当时实时汇率
   - ✅ 退款时从原订单 `t_dcc_info` 读 `exchange_rate`
   - 校验 SQL：JOIN 退款记录与原订单的 t_dcc_info（`fund_type='REFUND'` vs `fund_type='PURCHASE'`），比对 `exchange_rate` 是否一致，不一致即 MISMATCH。

2. **fund_type 区分用途**：
   - `PURCHASE` —— 原订单 DCC 信息
   - `REFUND` —— 退款时新生成的 DCC 信息（应复用原 rate）

3. **dcc_uptake 是关键状态**：
   - 用户接受 DCC → 走 DCC 流程，`t_dcc_info` 有完整数据
   - 用户不接受 DCC → 走原币种结算，可能没数据或数据为 0

4. **markup_rate 合规**：加点率不能过高（合规要求），不同币种对、不同商户费率不同。

5. **rebate_rate 商户返点**：是商户接入 DCC 的主要动力，鼓励商户引导用户选择 DCC。

6. **dcc_quote_id 来自第三方汇率源**：有效期通常 24h，过期需要重新询价。

7. **同币种不应该有 DCC**：如果 `order_currency == dcc_amount_cur`，说明数据异常。

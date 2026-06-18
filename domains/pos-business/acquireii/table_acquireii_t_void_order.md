---
id: tbl_acquireii_t_void_order
object_type: Table
domain: pos-business
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_void_order.md
tags:
- void
- 撤销
- 收单
subdomain: acquireii
module: null
sensitivity: normal
name: 撤销订单表
aliases:
- t_void_order
- acquireii.t_void_order
related_services: []
related_tables:
- tbl_acquireii_t_acquire_order
- tbl_acquireii_t_channel_param
- tbl_acquireii_t_payment_info
- tbl_acquireii_t_refund_order
- tbl_acquireii_t_reversal_order
- tbl_acquireii_t_reversal_orderii
- tbl_acquireii_t_revoke_order
- tbl_acquireii_t_stmt_event
- tbl_acquireii_t_void_ops_order
related_scenarios:
- scn_acquire_product_apply
- scn_merchant_transaction_db_check
- scn_payment_code_scanned_by_pos
- scn_payment_code_scanned_by_scanner
related_logs: []
related_requirements: []
related_failures: []
---

# t_void_order — 撤销订单表

## 一、用途与链路定位

记录收单订单的 **Void（撤销）** 操作。Void 通常发生在订单刚支付完成、**结算前**（T+0），资金尚未划走，直接取消，不产生退款流水。

**Void vs Refund vs Reversal vs Revoke**：
| 操作 | 时机 | 是否产生退款流水 | 关联表 |
|------|------|-----------------|--------|
| Void（撤销） | 结算前撤销 | 否 | `t_void_order` |
| Refund（退款） | 结算后退款 | 是，走完整退款流程 | `t_refund_order` |
| Reversal（反转） | 通信失败/异常时反向冲销 | 否 | `t_reversal_order` / `t_reversal_orderii` |
| Revoke（冲正） | 系统级冲正 | 否 | `t_revoke_order` |
| Void Ops（运营撤销） | 运营后台发起 | 否 | `t_void_ops_order` |

**典型场景**：
- 商户支付后立即发现错误调用 void
- POS 端"取消"操作（付款码被 POS/扫码枪扫场景）
- 24 小时内撤销（T+0 结算前）

**链路位置**：`t_acquire_order`（原订单）→ `t_void_order`（撤销）→ `t_stmt_event`（对账事件）。

## 二、字段清单

### 主键和关联
- `global_id` (bigint, PK)：void 全局号
- `acquire_global_id` (bigint, 必填)：原收单订单 global_id，关联 `t_acquire_order.global_id`
- `merchant_order_no` (varchar(200), 必填)：商户订单号（request_no）

### 业务方
- `partner_id` (varchar(200), 必填)：发起方 memberId
- `device_id` (varchar(200))：设备 ID

### Void 信息
- `void_type` (varchar(16))：void 类型
- `currency_code` (varchar(50), 必填)：币种
- `amount` (decimal(19,4), 必填)：金额
- `void_callback_url` (varchar(255))：void 回调地址

### 结算和手续费
- `settled_time` (timestamp(3))：结算时间
- `settlement_currency` (varchar(50))：结算币种
- `settlement_amount` (decimal(19,4))：结算金额
- `payee_fee_currency` (varchar(50))：void 手续费币种
- `payee_fee_amount` (decimal(19,4))：void 手续费

### 含税 / 不含税
- `pfbt_crcy` (varchar(50))：不含税金额币种
- `pfbt_amt` (decimal(19,4))：不含税金额
- `pfv_crcy` (varchar(50))：VAT 税币种
- `pf_vat` (decimal(19,4))：VAT 税

### 状态机
- `status` (varchar(32), 必填)：订单状态
- `fail_code` (varchar(50))：错误码
- `fail_message` (varchar(200))：错误描述
- `unity_result_code` (varchar(200))：统一结果码

### 其他
- `channel_param_id` (bigint)：渠道参数 ID，关联 `t_channel_param`
- `reserved` (varchar(200))：预留
- `created_time` / `last_updated_time` (timestamp(3))
- `data_version` (bigint)：数据版本

## 三、主键/索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | `global_id` | 主键 |
| `i_vo_aid` | `acquire_global_id` | 通过原订单查 void |
| `i_vo_ct` | `created_time` | 按时间查 |
| `i_vo_lut` | `last_updated_time` | 按更新时间扫 |
| `i_vo_mon` | `merchant_order_no` | 按商户订单号查 |

## 四、关联表

- `t_acquire_order` (N:1)：`acquire_global_id` → `global_id`，定位原始收单订单
- `t_channel_param` (N:1)：`channel_param_id` → 渠道参数
- `t_stmt_event`：void 完成后产生对账事件
- `t_payment_info`：原订单的支付信息可追溯
- `t_void_ops_order`：与运营侧撤销区分（用户/商户发起 vs 运营后台发起）
- `t_refund_order` / `t_reversal_order` / `t_revoke_order`：互斥的反向操作类型

## 五、QA 落库检查要点

1. **Void 必须在结算前**：若原订单已结算（`t_acquire_order.settled_time` 已置位），不应允许 void，需走 refund 流程。
2. **Void 是全额操作**：不支持部分 void，`amount` 应等于原订单金额，`currency_code` 与原订单币种一致。
3. **partner_id 一致性**：发起方 `partner_id` 必须与原 `t_acquire_order.partner_id` 一致，商户只能 void 自己的订单。
4. **手续费规则**：根据 `void_type` 不同，`payee_fee_amount` 处理规则不同（手续费可能不退）。
5. **状态机校验**：`status = 'FAILED'` 时必须有 `fail_code` / `fail_message`；成功态应有 `settled_time` 等结算字段。
6. **关联完整性**：`acquire_global_id` 必须对应已存在的 `t_acquire_order.global_id`。
7. **唯一性**：同一原订单（`acquire_global_id`）一般只应有一条成功的 void 记录，避免重复撤销。
8. **币种一致性**：`currency_code` 应与原订单币种一致；`settlement_currency` 与原订单结算币种一致。
9. **互斥校验**：同一 `acquire_global_id` 不应同时存在成功的 void 与 refund/reversal/revoke 记录。
10. **含税/不含税**：若原订单存在 VAT 税字段，void 时 `pfbt_amt`、`pf_vat` 应与原订单对应字段比例一致。

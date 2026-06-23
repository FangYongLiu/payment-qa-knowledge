---
id: tbl_acquireii_t_channel_param
object_type: Table
domain: device-pos
status: archived
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_channel_param.md
tags:
- 渠道参数
- ISO8583
- 卡组织
- ECI
subdomain: acquireii
module: null
sensitivity: normal
name: 渠道参数表
aliases:
- t_channel_param
- acquireii.t_channel_param
related_services: []
related_tables:
- tbl_acquireii_t_acquire_order
- tbl_acquireii_t_card_info
- tbl_acquireii_t_fiserv_channel_param
- tbl_acquireii_t_payment_info
- tbl_acquireii_t_refund_order
- tbl_acquireii_t_reversal_orderii
- tbl_acquireii_t_revoke_order
- tbl_acquireii_t_revoke_order_param
- tbl_acquireii_t_stmt_event
- tbl_acquireii_t_void_order
related_scenarios:
- scn_cko_standalone_card_binding
- scn_cko_subscription_test_cards
- scn_merchant_transaction_db_check
- scn_mit_autodebit
- scn_mit_cit_directpay_first
- scn_mit_cit_directpay_subsequent
- scn_mit_cit_payandsign
- scn_mit_cit_test_guide
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

`acquireii.t_channel_param`（渠道参数表，重要程度 ⭐⭐⭐⭐）记录订单走**非 Fiserv 渠道**（如 CKO、MPGS、Amex 等）时的**渠道层参数**，是收单链路上承载卡组织/渠道侧返回信息的核心明细表。

承载内容：
- 卡组织（Visa/MasterCard/Amex）授权号、交易号
- ISO 8583 渠道返回码
- 渠道方的 TID / MID / 渠道日期
- ECI 值（3D Secure 等级）
- Trace No、扩展信息

**典型场景**：
- 卡支付时记录卡组织返回的信息
- 后续退款 / 撤销 / 冲正时引用渠道方信息
- 与卡组织/渠道方对账时核对授权号、Trace No

## 在交易链路中的位置

```
t_acquire_order (主单)
   ├── channel_param_id ──► t_channel_param (本表，非 Fiserv 渠道)
   └── 或 fiserv_channel_param_id ──► t_fiserv_channel_param (Fiserv 渠道)

t_payment_info / t_refund_order / t_void_order / t_reversal_orderii
   └── channel_param_id ──► t_channel_param
```

本表与 `t_fiserv_channel_param` 互斥使用：根据订单实际走的渠道，二选一挂载。

## 关键列

### 主键
- `id` bigint，**主键**，必填

### 卡组织授权信息
- `card_authorization_no` varchar(32)：卡组织授权号
- `card_transaction_no` varchar(32)：卡组织交易号

### ISO 8583 协议字段
- `ios_response_code` varchar(128)：ISO 8583 响应码（`00` = 成功）
- `tpdu_response_ues_token` varchar(32)：TPDU 响应 Token

### 渠道信息
- `channel_code` varchar(16)：渠道代码
- `channel_tid` varchar(64)：渠道 TID
- `channel_mid` varchar(64)：渠道 MID
- `channel_date` varchar(64)：渠道日期
- `amex_mid` varchar(32)：Amex MID

### 其他
- `trace_no` varchar(64)：跟踪号（与卡组织对账时使用）
- `eci_value` varchar(64)：ECI 值（3D Secure 验证结果）
- `extension` varchar(1024)：扩展信息
- `created_time` timestamp(3)：创建时间

## 主键 / 索引
- PRIMARY：`id`

## 关联关系（被引用，N:1）

以下表通过 `channel_param_id` 外键关联到本表：
- `t_acquire_order`（部分场景，主单直接挂渠道参数）
- `t_payment_info`（支付明细，最常见的引用方）
- `t_refund_order`（退款单引用原渠道返回信息）
- `t_void_order`（撤销单引用原渠道返回信息）
- `t_reversal_orderii`（冲正单引用原渠道返回信息）

相关同体系表：
- `t_fiserv_channel_param`：Fiserv 渠道的对应表，与本表互斥
- `t_card_info`：卡信息表，配合本表完整描述卡支付链路
- `t_stmt_event`：对账事件，依赖本表的 `trace_no` / `card_authorization_no` 进行渠道对账

## QA 落库检查要点

1. **ECI 值含义校验**：
   - `05`：3D Secure 通过（持卡人验证）
   - `06`：商户尝试 3D 但不可用
   - `07`：未尝试 3D
   - 检查 3D Secure 测试场景下 ECI 是否符合预期。
2. **ios_response_code**：ISO 8583 标准响应码。`00` 为成功，非 `00` 为失败；需对渠道错误码做统计归类，并校验上游订单状态与之一致。
3. **trace_no**：用于交易追踪，与卡组织对账核对，需保证唯一可追溯，不应为空。
4. **授权号一致性**：退款 / 撤销 / 冲正单引用的 `t_channel_param` 中的 `card_authorization_no`、`card_transaction_no` 应与原支付单一致或可追溯到原单。
5. **extension** 长度上限 1024 字节，校验存储不溢出。
6. **链路一致性**：`t_acquire_order` → `t_payment_info` → `t_channel_param` 的 `channel_code`、`channel_tid`、`channel_mid` 应保持一致。
7. **渠道互斥**：同一订单不应同时挂载 `t_channel_param` 与 `t_fiserv_channel_param`，需校验 `channel_param_id` 与 `fiserv_channel_param_id` 二选一。
8. **MIT/CIT 场景**：DirectPay、PayAndSign、AutoDebit 等签约/代扣场景下，首次 CIT 与后续 MIT 都需正确落库渠道返回的授权信息，便于关联与对账。
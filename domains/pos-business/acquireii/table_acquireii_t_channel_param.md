---
id: tbl_acquireii_t_channel_param
object_type: Table
domain: pos-business
status: active
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
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
记录订单走具体支付渠道（非 Fiserv）时的**渠道层参数**，表名 `acquireii.t_channel_param`，重要程度 ⭐⭐⭐⭐。

包括：
- 卡组织（Visa/MasterCard）授权号、交易号
- 渠道返回码（ISO 8583）
- 渠道方的 TID / MID
- 渠道日期
- ECI 值（3D Secure 等级）

**典型场景**：
- 卡支付时记录卡组织返回的信息
- 后续退款 / 撤销时引用渠道方信息
- 对账时和渠道方核对

## 关键列

### 主键
- `id` bigint，**主键**，必填

### 卡组织授权信息
- `card_authorization_no` varchar(32)：卡组织授权号
- `card_transaction_no` varchar(32)：卡组织交易号

### ISO 8583 协议字段
- `ios_response_code` varchar(128)：ISO 8583 响应码（00 = 成功）
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

## 主键/索引
- PRIMARY：`id`（主键）

被以下表通过 `channel_param_id` 关联（N:1）：
- `t_acquire_order`（部分场景）
- `t_refund_order`
- `t_void_order`
- `t_payment_info`
- `t_reversal_orderii`

## 校验点(QA 关注)
1. **ECI 值含义**：
   - 05：3D Secure 通过
   - 06：商户尝试 3D 但不可用
   - 07：未尝试 3D
2. **ios_response_code**：ISO 8583 标准响应码，`00` 为成功，非 `00` 为失败，需校验渠道错误码统计与归类。
3. **trace_no**：用于交易追踪，与卡组织对账时使用，需保证可追溯。
4. **extension** 长度上限 1024 字节，可存较长扩展信息。
5. 关联校验：上游订单表通过 `channel_param_id` 引用本表，QA 需确认链路上 `t_payment_info` → `t_channel_param` 数据一致性。

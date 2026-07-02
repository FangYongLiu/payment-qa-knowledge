---
id: scn_pos_transaction_db_check
object_type: Scenario
name: POS刷卡交易落库检查
aliases:
- POS交易检查哪些表
- Fiserv落库校验
- pos transaction db check
domain: offline-business
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-06-25'
source_type: manual
source_ref: hub/pos-transaction-db-check
tags:
- POS
- Fiserv
- 刷卡交易
- 落库校验
- 结算
- QA
related_services: [svc_acquireii, svc_device]
related_tables:
- tbl_fiserv_sale_order
- tbl_fiserv_sale_void_ops_order
- tbl_fiserv_reversal_order
- tbl_fiserv_refund_order
- tbl_fiserv_batch
- tbl_pos_settlement
- tbl_pos_settlement_history
- tbl_acquire_terminal
- tbl_pcc_content
- tbl_merchant_device
- tbl_device_apply_order
- tbl_active_code
- tbl_hardware_info
- tbl_acquireii_t_acquire_order
- tbl_acquireii_t_payment_info
- tbl_acquireii_t_fiserv_channel_param
- tbl_acquireii_t_terminal_detail
related_logs: []
---

# POS刷卡交易落库检查

## 触发 / 入口
一笔 POS 刷卡交易(Fiserv 渠道:销售/撤销/冲正/退款)或 POS 结算完成后，QA 校验各表落库与跨表关联。

## 关联关系
- **涉及服务**:[[svc_acquireii]](收单/Fiserv 交易与结算)、[[svc_device]](设备/终端绑定)(= `related_services`)。
- **校验的表**:Fiserv 交易族 [[tbl_fiserv_sale_order]] / [[tbl_fiserv_sale_void_ops_order]] / [[tbl_fiserv_reversal_order]] / [[tbl_fiserv_refund_order]] / [[tbl_fiserv_batch]];结算 [[tbl_pos_settlement]] / [[tbl_pos_settlement_history]];终端/设备 [[tbl_acquire_terminal]] / [[tbl_acquireii_t_terminal_detail]] / [[tbl_merchant_device]] / [[tbl_hardware_info]] / [[tbl_active_code]] / [[tbl_device_apply_order]];凭证/渠道 [[tbl_pcc_content]] / [[tbl_acquireii_t_fiserv_channel_param]];收单主链路 [[tbl_acquireii_t_acquire_order]] / [[tbl_acquireii_t_payment_info]](= `related_tables`)。

## 前置条件
- POS 终端已激活并绑定商户(设备激活流程，详见 [[flow_device_activation]])。
- 完成一笔刷卡交易，拿到 orderNo / Fiserv RRN / TID / batchNo 等关联键。

## 操作步骤
1. 按交易类型定位 Fiserv 主单表。
2. 沿 RRN/TID/batch 关联键核对金额、状态、卡信息、终端。
3. 结算阶段核对 POS 结算表与历史。
4. 设备/终端维度核对绑定与硬件信息。

## DB 校验点
- **Fiserv 交易**:[[tbl_fiserv_sale_order]](销售)/ [[tbl_fiserv_sale_void_ops_order]](撤销)/ [[tbl_fiserv_reversal_order]](冲正)/ [[tbl_fiserv_refund_order]](退款);批次 [[tbl_fiserv_batch]]。
- **结算**:[[tbl_pos_settlement]] + [[tbl_pos_settlement_history]]。
- **终端/设备**:[[tbl_acquire_terminal]] / [[tbl_acquireii_t_terminal_detail]] / [[tbl_merchant_device]](商户-设备绑定)/ [[tbl_hardware_info]] / [[tbl_active_code]](激活码)/ [[tbl_device_apply_order]](申请单)。
- **凭证/渠道**:[[tbl_pcc_content]](支付授权凭证)/ [[tbl_acquireii_t_fiserv_channel_param]](渠道参数)。
- **关联收单主链路**:[[tbl_acquireii_t_acquire_order]] / [[tbl_acquireii_t_payment_info]]。

## 预期结果
Fiserv 各表落库完整、状态一致、与收单主单/结算金额对齐、终端绑定有效、关联键可追溯。

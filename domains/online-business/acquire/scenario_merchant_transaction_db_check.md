---
id: scn_merchant_transaction_db_check
object_type: Scenario
name: 商户交易落库检查
domain: merchant-acquisition-testing
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: manual
source_ref: hub/merchant-transaction-db-check
tags:
- 交易
- 落库校验
- 收单
- POS
- QA
aliases:
- 商户交易需要检查哪些表
- 交易落库校验
- transaction db check
related_tables:
- tbl_acquireii_t_acquire_order
- tbl_acquireii_t_payment_info
- tbl_acquireii_t_amount_detail
- tbl_acquireii_t_goods_detail
- tbl_acquireii_t_card_info
- tbl_acquireii_t_dcc_info
- tbl_acquireii_t_dcc_info_log
- tbl_acquireii_t_refund_order
- tbl_acquireii_t_reversal_order
- tbl_acquireii_t_reversal_orderii
- tbl_acquireii_t_void_order
- tbl_acquireii_t_void_ops_order
- tbl_acquireii_t_revoke_order
- tbl_acquireii_t_preauth_control
- tbl_acquireii_t_preauth_relation
- tbl_acquireii_t_deposit_order
- tbl_acquireii_t_sharing_info
- tbl_acquireii_t_promotion_info
- tbl_acquireii_t_secondary_merchant_detail
- tbl_acquireii_t_terminal_detail
- tbl_acquire_terminal
- tbl_acquire_extension
- tbl_fiserv_sale_order
- tbl_fiserv_sale_void_ops_order
- tbl_fiserv_reversal_order
- tbl_fiserv_refund_order
- tbl_pos_settlement
---

## 触发/入口
一笔商户交易（收单/退款/冲正/撤销/预授权/DCC/POS）完成后，QA 需要校验各链路的数据库落库是否正确、跨表关联是否一致。

## 前置条件
- 已通过 API 或 POS 终端发起并完成一笔交易
- 拿到 `merchantOrderNo` / `orderNo` / `paymentSeqNo` / `preauthOrderNo` 等关联键

## 操作步骤
1. 按交易类型定位主表（见下「DB 校验点」分组）
2. 沿关联键逐表核对：金额、状态、币种、商户/终端、时间戳
3. 关联明细表（金额/商品/卡/DCC）与主单一致性
4. 出款/分账/营销等下游表按需核对

## DB 校验点
- **收单主链路**：`t_acquire_order`（订单）→ `t_payment_info`（支付）→ `t_amount_detail`/`t_goods_detail`/`t_card_info`（明细）
- **DCC**：`t_dcc_info`（订单维度）/ `t_dcc_info_log`（报价维度，多次报价）
- **退款/冲正/撤销/撤单**：`t_refund_order` / `t_reversal_order`(+`ii`) / `t_void_order`+`t_void_ops_order` / `t_revoke_order`
- **预授权**：`t_preauth_control` + `t_preauth_relation`（PreAuth 不产生 Fund Flow，Capture 才产生）
- **POS/Fiserv**：`tbl_fiserv_sale_order` / `tbl_fiserv_sale_void_ops_order` / `tbl_fiserv_reversal_order` / `tbl_fiserv_refund_order`；结算 `t_pos_settlement`
- **商户/终端**：`t_secondary_merchant_detail` / `t_terminal_detail` / `t_acquire_terminal` / `t_acquire_extension`
- **充值/分账/营销**：`t_deposit_order` / `t_sharing_info` / `t_promotion_info`

## 预期结果
各表落库完整、状态终态一致、金额与币种逐表对齐、关联键全链路可追溯、无悬挂记录。

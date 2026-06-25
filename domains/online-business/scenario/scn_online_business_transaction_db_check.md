---
id: scn_online_business_transaction_db_check
object_type: Scenario
name: 商户交易落库检查 (Transaction DB Check)
aliases: [商户交易需要检查哪些表, 交易落库校验, transaction db check]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: manual
source_ref: hub/merchant-transaction-db-check
tags: [online-business, 收单, 交易, 落库校验, POS, QA]
related_services: [svc_acquireii]
related_tables: [tbl_acquireii_t_acquire_order, tbl_acquireii_t_payment_info, tbl_acquireii_t_amount_detail, tbl_acquireii_t_goods_detail, tbl_acquireii_t_card_info, tbl_acquireii_t_dcc_info, tbl_acquireii_t_dcc_info_log, tbl_acquireii_t_refund_order, tbl_acquireii_t_reversal_order, tbl_acquireii_t_reversal_orderii, tbl_acquireii_t_void_order, tbl_acquireii_t_void_ops_order, tbl_acquireii_t_revoke_order, tbl_acquireii_t_preauth_control, tbl_acquireii_t_preauth_relation, tbl_acquireii_t_deposit_order, tbl_acquireii_t_sharing_info, tbl_acquireii_t_promotion_info, tbl_acquireii_t_secondary_merchant_detail, tbl_acquireii_t_terminal_detail, tbl_acquireii_t_fiserv_refund_bucket]
related_logs: []
---

# 商户交易落库检查 (Transaction DB Check)

## 触发 / 入口
一笔商户交易(收单 / 退款 / 冲正 / 撤销 / 预授权 / DCC / POS)完成后,QA 需校验各链路的数据库落库是否正确、跨表关联是否一致。

## 关联关系
- **涉及服务**:[[svc_acquireii]](= `related_services`,收单主服务)。
- **校验的表**:见 `related_tables` —— 收单主链路与各类型订单表(收单/退款/冲正/撤销/撤单/预授权/DCC/充值/分账/营销/商户终端)及 [[tbl_acquireii_t_fiserv_refund_bucket]]。Fiserv POS 表 `t_fiserv_sale_order` / `t_fiserv_sale_void_ops_order` / `t_fiserv_reversal_order` / `t_fiserv_refund_order`、结算表 `t_pos_settlement`、终端扩展 `t_acquire_terminal` / `t_acquire_extension` 对象待补。
- **相关日志**:待补。

## 前置条件
- 已通过 API 或 POS 终端发起并完成一笔交易。
- 拿到 `merchantOrderNo` / `orderNo` / `paymentSeqNo` / `preauthOrderNo` 等关联键。

## 操作步骤
1. 按交易类型定位主表(见下「DB 校验点」分组)。
2. 沿关联键逐表核对:金额、状态、币种、商户 / 终端、时间戳。
3. 关联明细表(金额 / 商品 / 卡 / DCC)与主单一致性。
4. 出款 / 分账 / 营销等下游表按需核对。

## DB 校验点
- **收单主链路**:[[tbl_acquireii_t_acquire_order]](订单)→ [[tbl_acquireii_t_payment_info]](支付)→ [[tbl_acquireii_t_amount_detail]] / [[tbl_acquireii_t_goods_detail]] / [[tbl_acquireii_t_card_info]](明细)。
- **DCC**:[[tbl_acquireii_t_dcc_info]](订单维度)/ [[tbl_acquireii_t_dcc_info_log]](报价维度,多次报价)。
- **退款 / 冲正 / 撤销 / 撤单**:[[tbl_acquireii_t_refund_order]] / [[tbl_acquireii_t_reversal_order]](+[[tbl_acquireii_t_reversal_orderii]])/ [[tbl_acquireii_t_void_order]]+[[tbl_acquireii_t_void_ops_order]] / [[tbl_acquireii_t_revoke_order]]。
- **预授权**:[[tbl_acquireii_t_preauth_control]] + [[tbl_acquireii_t_preauth_relation]](PreAuth 不产生 Fund Flow,Capture 才产生)。
- **POS / Fiserv**:`t_fiserv_sale_order` / `t_fiserv_sale_void_ops_order` / `t_fiserv_reversal_order` / `t_fiserv_refund_order`;退款资金桶 [[tbl_acquireii_t_fiserv_refund_bucket]];结算 `t_pos_settlement`(部分表对象待补)。
- **商户 / 终端**:[[tbl_acquireii_t_secondary_merchant_detail]] / [[tbl_acquireii_t_terminal_detail]];`t_acquire_terminal` / `t_acquire_extension`(待补)。
- **充值 / 分账 / 营销**:[[tbl_acquireii_t_deposit_order]] / [[tbl_acquireii_t_sharing_info]] / [[tbl_acquireii_t_promotion_info]]。

## 预期结果
各表落库完整、状态终态一致、金额与币种逐表对齐、关联键全链路可追溯、无悬挂记录。

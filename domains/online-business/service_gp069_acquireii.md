---
id: svc_acquireii
object_type: Service
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp069
name: acquireii
subdomain: acquiring
dev_owner: Sijia.Zhang
aliases: [gp069_acquireii]
related_services: [svc_tradeii, svc_voucher, svc_cmf, svc_ppcenter, svc_ues_ws, svc_member, svc_marketing, svc_device, svc_merchant, svc_offline_payment, svc_deposit]
related_tables: []
---

# acquireii

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp069` · domain=`online-business`。

## 作用
收单核心（Acquire II）—— 商户订单受理 / 下单 / 退款受理，编排 tradeii、voucher、ppcenter、marketing、member

## 系统中的位置
- 功能层:收单 / 收银 (Acquiring / Cashier)
- 业务域:`online-business`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_tradeii]] tradeii（交易订单引擎） · 65005 次 · high
- [[svc_voucher]] voucher（全局 ID 与幂等凭证） · 29547 次 · high
- [[svc_cmf]] cmf（渠道管理与资金） · 22731 次 · high
- [[svc_ppcenter]] ppcenter（产品中心） · 17622 次 · high
- [[svc_ues_ws]] ues-ws（用户事件 / 数据服务） · 9100 次 · med·待核实
- [[svc_member]] member（会员 / 账户核心） · 5124 次 · high
- [[svc_marketing]] marketing（营销服务） · 4365 次 · high
- [[svc_device]] device（设备 / 产品中心接入） · 4008 次 · high
- [[svc_merchant]] merchant（商户主数据 / 商户管理） · 2031 次 · high
- [[svc_offline_payment]] offline-payment（线下支付） · 654 次 · high
- [[svc_deposit]] deposit（充值 / 存款服务） · 123 次 · high

**被调用(上游)—— 这些服务调用本服务:**
merchant-frontend

## 涉及的 API / 数据库表
**读写的表:** [[tbl_acquireii_t_refund_order]] 退款订单表、[[tbl_acquireii_t_payment_info]] 支付信息表 (t_payment_info)、[[tbl_acquireii_t_fiserv_channel_param]] Fiserv渠道参数表、[[tbl_acquireii_t_promotion_info]] 优惠券信息表 t_promotion_info、[[tbl_acquireii_t_sharing_info]] 分账信息表、[[tbl_acquireii_t_revoke_order]] 冲正订单表、[[tbl_acquireii_t_card_info]] 支付卡信息表、[[tbl_acquireii_t_secondary_merchant_detail]] 二级商户明细表、[[tbl_acquireii_t_event_param]] 事件参数表 (t_event_param)、[[tbl_acquireii_t_dcc_info_log]] DCC信息日志表、[[tbl_acquireii_t_inst_code_config]] 机构代码配置表、[[tbl_acquireii_t_channel_param]] 渠道参数表、[[tbl_acquireii_t_revoke_order_param]] 冲正订单参数表、[[tbl_acquireii_t_stmt_event]] 对账事件表 (t_stmt_event)、[[tbl_acquireii_t_dcc_info]] DCC信息表 t_dcc_info、[[tbl_acquireii_t_void_order]] 撤销订单表、[[tbl_acquireii_t_command_param]] 指令参数表、[[tbl_acquireii_t_pay_scene_param]] 支付场景参数表、[[tbl_acquireii_t_command]] 指令表 t_command、[[tbl_acquireii_t_preauth_control]] 预授权控制表、[[tbl_acquireii_t_void_ops_order]] 运营撤销订单表、[[tbl_acquireii_t_preauth_relation]] 预授权关系表 t_preauth_relation、[[tbl_acquireii_t_deposit_order]] 充值订单表、[[tbl_acquireii_t_sequence_table]] 序号生成表、[[tbl_acquireii_t_reversal_orderii]] Reversal Order II 表、[[tbl_acquireii_t_request_identity]] 请求标识表、[[tbl_acquireii_t_acquire_order]] 收单订单主表 t_acquire_order、[[tbl_acquireii_t_terminal_detail]] 终端明细表、[[tbl_acquireii_t_reversal_order]] Reversal订单表、[[tbl_acquireii_t_unretryable_command]] 不可重试指令表、[[tbl_acquireii_t_goods_detail]] 商品明细表、[[tbl_acquireii_t_retryable_command]] 可重试指令表、[[tbl_acquireii_t_amount_detail]] 金额明细表

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）

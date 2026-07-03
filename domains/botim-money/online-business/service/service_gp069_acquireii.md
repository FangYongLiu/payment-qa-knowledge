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
related_services: [svc_tradeii, svc_voucher, svc_cmf, svc_ppcenter, svc_ues_ws, svc_member, svc_marketing, svc_device, svc_merchant, svc_offline_payment, svc_deposit, svc_wechat_channel]
related_tables: []
related_scenarios: [scn_online_business_cashier_pay, scn_online_business_direct_pay, scn_online_business_pre_auth]
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
- [[svc_wechat_channel]] wechat-channel（微信渠道） · 360 次 · high（UAT 2026-07-03 实测,`WechatClientImpl`）

**被调用(上游)—— 这些服务调用本服务:**
merchant-frontend

## 涉及的 API / 数据库表
**读写的表:** [[tbl_acquireii_t_refund_order]] 退款订单表、[[tbl_acquireii_t_payment_info]] 支付信息表 (t_payment_info)、[[tbl_acquireii_t_fiserv_channel_param]] Fiserv渠道参数表、[[tbl_acquireii_t_promotion_info]] 优惠券信息表 t_promotion_info、[[tbl_acquireii_t_sharing_info]] 分账信息表、[[tbl_acquireii_t_revoke_order]] 冲正订单表、[[tbl_acquireii_t_card_info]] 支付卡信息表、[[tbl_acquireii_t_secondary_merchant_detail]] 二级商户明细表、[[tbl_acquireii_t_event_param]] 事件参数表 (t_event_param)、[[tbl_acquireii_t_dcc_info_log]] DCC信息日志表、[[tbl_acquireii_t_inst_code_config]] 机构代码配置表、[[tbl_acquireii_t_channel_param]] 渠道参数表、[[tbl_acquireii_t_revoke_order_param]] 冲正订单参数表、[[tbl_acquireii_t_stmt_event]] 对账事件表 (t_stmt_event)、[[tbl_acquireii_t_dcc_info]] DCC信息表 t_dcc_info、[[tbl_acquireii_t_void_order]] 撤销订单表、[[tbl_acquireii_t_command_param]] 指令参数表、[[tbl_acquireii_t_pay_scene_param]] 支付场景参数表、[[tbl_acquireii_t_command]] 指令表 t_command、[[tbl_acquireii_t_preauth_control]] 预授权控制表、[[tbl_acquireii_t_void_ops_order]] 运营撤销订单表、[[tbl_acquireii_t_preauth_relation]] 预授权关系表 t_preauth_relation、[[tbl_acquireii_t_deposit_order]] 充值订单表、[[tbl_acquireii_t_sequence_table]] 序号生成表、[[tbl_acquireii_t_reversal_orderii]] Reversal Order II 表、[[tbl_acquireii_t_request_identity]] 请求标识表、[[tbl_acquireii_t_acquire_order]] 收单订单主表 t_acquire_order、[[tbl_acquireii_t_terminal_detail]] 终端明细表、[[tbl_acquireii_t_reversal_order]] Reversal订单表、[[tbl_acquireii_t_unretryable_command]] 不可重试指令表、[[tbl_acquireii_t_goods_detail]] 商品明细表、[[tbl_acquireii_t_retryable_command]] 可重试指令表、[[tbl_acquireii_t_amount_detail]] 金额明细表

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[auto_online_business_bpg_paypage]](自动化:收银台 BPG PayPage 自动化)
- [[auto_online_business_direct_pay]](自动化:直连支付自动化)
- [[auto_online_business_dynqr]](自动化:动态二维码收银自动化)
- [[auto_online_business_pre_auth_capture]](自动化:预授权/请款自动化)
- [[auto_online_business_qr_pay]](自动化:二维码/付款码开关自动化)
- [[auto_online_business_send_pay_link]](自动化:发送支付链接自动化)
- [[auto_online_business_smart_code]](自动化:智慧码支付自动化)
- [[auto_online_business_smart_pos]](自动化:智能 POS 自动化)
- [[auto_online_business_taxi]](自动化:出租车支付自动化)
- [[flow_cashier_payment]](流程:收银台 / 收单卡支付端到端流程（含退款）)
- [[flow_pos_scan_payment_code]](流程:付款码被 POS 机扫(线下被扫收单)端到端流程)
- [[scn_online_business_cashier_pay]](场景:收银台支付 (Cashier / PayPage))
- [[scn_online_business_direct_pay]](场景:直连支付 (Direct Pay))
- [[scn_online_business_mpgs_channel]](场景:MPGS 渠道卡支付(3DS2 / MOTO / 设备支付 / 卡组织拆分 / 退款Void))
- [[scn_online_business_openapi_protocol_signing]](场景:商户 Open API 接入协议与签名/加密规则)
- [[scn_online_business_payment_code_scan]](场景:付款码被扫线下收单 (POS / 扫码枪))
- [[scn_online_business_pre_auth]](场景:预授权 / 请款 (PreAuth-Capture))
- [[scn_online_business_transaction_db_check]](场景:商户交易落库检查 (Transaction DB Check))
- [[scn_pos_transaction_db_check]](场景:POS刷卡交易落库检查)
- [[ts_acquire_order_slow_sql]](排障:收单订单查询慢SQL(t_acquire_order 大商户时间范围查询))

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp069` · domain=`online-business`。

## 涉及的表(DB)
本服务读写 `acquireii` 库(48 张,见 `online-business/table/acquireii/`)。主要表:[[tbl_acquireii_t_acquire_order]] · [[tbl_acquireii_t_amount_detail]] · [[tbl_acquireii_t_deposit_order]] · [[tbl_acquireii_t_fiserv_batch]] · [[tbl_acquireii_t_fiserv_refund_order]] · [[tbl_acquireii_t_fiserv_reversal_order]]。

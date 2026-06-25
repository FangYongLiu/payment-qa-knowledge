---
id: svc_remittance
object_type: Service
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp188
name: remittance
dev_owner: Wujiang.Ding
aliases: [gp188_remittance]
related_services: [svc_member, svc_router, svc_acs, svc_cms, svc_grc_check_identity_provider, svc_paylater, svc_tradeii, svc_voucher, svc_pns, svc_reconciliation, svc_query, svc_aml, svc_protocol, svc_ufs2]
related_scenarios: [scn_online_business_merchant_payout, scn_remittance_cross_border]
related_tables:
- tbl_remittance_leaf_alloc
- tbl_remittance_t_additional_info_field
- tbl_remittance_t_back_report_task
- tbl_remittance_t_bank_code
- tbl_remittance_t_bank_info
- tbl_remittance_t_basic_channel_order
- tbl_remittance_t_basic_order
- tbl_remittance_t_beneficiary_account_info
- tbl_remittance_t_beneficiary_address
- tbl_remittance_t_beneficiary_check
- tbl_remittance_t_beneficiary_identity_info
- tbl_remittance_t_beneficiary_statics_total
- tbl_remittance_t_branch_info
- tbl_remittance_t_channel_activity
- tbl_remittance_t_channel_balance
- tbl_remittance_t_channel_balance_v
- tbl_remittance_t_channel_config
- tbl_remittance_t_channel_currency_config
- tbl_remittance_t_channel_field_config
- tbl_remittance_t_channel_market
- tbl_remittance_t_channel_money_limitation
- tbl_remittance_t_channel_notify
- tbl_remittance_t_channel_notify_his
- tbl_remittance_t_channel_order
- tbl_remittance_t_channel_param_mapping
- tbl_remittance_t_channel_quotation_strategy
- tbl_remittance_t_channel_quotation_strategy_his
- tbl_remittance_t_channel_return_code
- tbl_remittance_t_channel_session
- tbl_remittance_t_channel_sftp_config
- tbl_remittance_t_channel_tips
- tbl_remittance_t_charge_strategy
- tbl_remittance_t_compensation_event
- tbl_remittance_t_corridor_fail_log
- tbl_remittance_t_corridor_fail_show_config
- tbl_remittance_t_corridor_msg_config
- tbl_remittance_t_country_config
- tbl_remittance_t_currency_blacklist
- tbl_remittance_t_currency_config
- tbl_remittance_t_currency_country_config
- tbl_remittance_t_data_dict
- tbl_remittance_t_dealing_record
- tbl_remittance_t_delivery_time_stats
- tbl_remittance_t_dyn_cohort
- tbl_remittance_t_dyn_cohort_config
- tbl_remittance_t_dyn_cohort_rule
- tbl_remittance_t_dyn_exec_log
- tbl_remittance_t_dyn_operation_history
- tbl_remittance_t_dyn_quote_log
- tbl_remittance_t_dyn_rule
- tbl_remittance_t_dyn_strategy
- tbl_remittance_t_dyn_strategy_cohort_mapping
- tbl_remittance_t_dyn_strategy_stat
- tbl_remittance_t_dynamic_field
- tbl_remittance_t_evaluate
- tbl_remittance_t_event_config
- tbl_remittance_t_exchange_rate_history
- tbl_remittance_t_exchange_rate_record
- tbl_remittance_t_exchange_rate_statistics
- tbl_remittance_t_field_mapping
- tbl_remittance_t_field_validate_result
- tbl_remittance_t_flow_difference
- tbl_remittance_t_funding_record
- tbl_remittance_t_hold_order_task
- tbl_remittance_t_hold_report_record
- tbl_remittance_t_i18n
- tbl_remittance_t_market_order
- tbl_remittance_t_member_property
- tbl_remittance_t_member_relationship
- tbl_remittance_t_notification_config
- tbl_remittance_t_notification_event
- tbl_remittance_t_notification_record
- tbl_remittance_t_order
- tbl_remittance_t_order_aae
- tbl_remittance_t_order_event
- tbl_remittance_t_out_market_rate
- tbl_remittance_t_popup_control
- tbl_remittance_t_proper_charge_strategy
- tbl_remittance_t_public_notice
- tbl_remittance_t_quotation_strategy
- tbl_remittance_t_rate_alert
- tbl_remittance_t_rate_alert_history
- tbl_remittance_t_rate_crawl_data
- tbl_remittance_t_refund_order
- tbl_remittance_t_remittance_alert
- tbl_remittance_t_remittance_config
- tbl_remittance_t_remittance_limit
- tbl_remittance_t_remittance_report_schedule
- tbl_remittance_t_remittance_report_task
- tbl_remittance_t_remittance_time
- tbl_remittance_t_revaluation_rate
- tbl_remittance_t_sender_statics_total
- tbl_remittance_t_submit_additional_info
- tbl_remittance_t_success_rate_log
- tbl_remittance_t_todo_log
---

# remittance

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp188` · domain=`remittance`。

## 作用
跨境汇款核心 —— 编排 member/router/acs/tradeii/reconciliation + 各汇款渠道（terrapay/arp/fuze）

## 系统中的位置
- 功能层:汇款 (Remittance)
- 业务域:`remittance`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_member]] member（会员 / 账户核心） · 5703405 次 · high
- [[svc_router]] router（渠道路由） · 4379425 次 · high
- [[svc_acs]] acs（反欺诈 / 风控 + 渠道密钥） · 41081 次 · high
- [[svc_cms]] cms（内容 / 配置管理） · 20629 次 · high
- [[svc_grc_check_identity_provider]] grc-check-identity-provider（风控合规身份校验） · 15935 次 · med·待核实
- [[svc_paylater]] paylater · 7718 次 · high
- [[svc_tradeii]] tradeii（交易订单引擎） · 6862 次 · high
- [[svc_voucher]] voucher（全局 ID 与幂等凭证） · 5007 次 · high
- [[svc_pns]] pns（支付通知服务） · 1940 次 · high
- [[svc_reconciliation]] reconciliation（对账） · 1820 次 · high
- [[svc_query]] query（查询 / 报表服务） · 1724 次 · high
- [[svc_aml]] aml（反洗钱） · 613 次 · high
- [[svc_protocol]] protocol（代扣 / 签约协议管理） · 205 次 · high
- [[svc_ufs2]] ufs2（用户文件 / 数据服务） · 181 次 · med·待核实

**被调用(上游)—— 这些服务调用本服务:**
fcw

## 参与的业务场景(cgs 回归)
- §7. 跨境汇款（toC，`test_remittance`）

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[auto_online_business_transfer_order]](自动化:转账下单自动化)
- [[auto_online_business_transfer_to_bank]](自动化:转账到银行自动化)
- [[auto_online_business_transfer_to_card]](自动化:转账到卡自动化)
- [[auto_remittance_remittance]](自动化:跨境汇款自动化)
- [[auto_remittance_vam]](自动化:VAM 虚拟账户自动化)
- [[flow_cashier_payment]](流程:收银台 / 收单卡支付端到端流程（含退款）)
- [[scn_online_business_merchant_payout]](场景:商户出款 / 转账 (Transfer / Payout))
- [[scn_remittance_cross_border]](场景:跨境汇款 (Remittance))
- [[scn_remittance_rate_alert]](场景:汇率提醒(Rate Alert))

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp188` · domain=`remittance`。

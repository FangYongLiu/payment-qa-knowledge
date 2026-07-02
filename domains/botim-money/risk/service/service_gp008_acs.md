---
id: svc_acs
object_type: Service
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp008
name: acs
dev_owner: Yongxing.Cao
aliases: [gp008_acs]
related_services: []
related_scenarios: [scn_online_business_direct_pay, scn_online_business_pre_auth]
related_tables:
- tbl_acs_db
- tbl_acs_leaf_alloc
- tbl_acs_t_api_config
- tbl_acs_t_api_mgr
- tbl_acs_t_api_mgr_group
- tbl_acs_t_basic_group
- tbl_acs_t_gateway_api_config
- tbl_acs_t_gateway_api_group
- tbl_acs_t_gateway_api_group_relation
- tbl_acs_t_gateway_merchant_api_auth
- tbl_acs_t_group_relation
- tbl_acs_t_key_config
- tbl_acs_t_language_config
- tbl_acs_t_merchant_api_auth
- tbl_acs_t_merchant_api_support
- tbl_acs_t_merchant_config_template
- tbl_acs_t_merchant_fo_setting
- tbl_acs_t_merchant_funds
- tbl_acs_t_merchant_inner_account
- tbl_acs_t_merchant_key
- tbl_acs_t_merchant_setting
- tbl_acs_t_operation_config
- tbl_acs_t_outer_code
- tbl_acs_t_rate_limit_config
- tbl_acs_t_rate_limit_group
- tbl_acs_t_reffer_list
- tbl_acs_t_setting_attribute
- tbl_acs_t_template_account
- tbl_acs_t_template_auth
- tbl_acs_t_template_auth_group
- tbl_acs_t_translate_config
- tbl_acs_t_unity_code_mapping
- tbl_acs_t_wh_key
- tbl_acs_t_withhold_auth
- tbl_acs_t_withhold_auth_log
---

# acs

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp008` · domain=`risk`。

## 作用
反欺诈 / 风控 + 渠道密钥（ACS，queryPartnerKey）—— 被渠道 / 收单 / 出款 / 汇款广泛调用

## 系统中的位置
- 功能层:风控 / 合规 / KYC (Risk / Compliance / KYC)
- 业务域:`risk`

## 关联关系

**被调用(上游)—— 这些服务调用本服务:**
wechat-channel, pbs, iso8583-gateway, fundout, tradeii, marketing-event

## 涉及的 API / 数据库表
**读写的表:** [[tbl_acs_db]] 网关库(acs)核心表

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）
- §3. 自动代扣 / 签约（`test_auto_debit`）
- §5. 银行/卡转账、出款（`test_transfer_to_bank` / `test_transfer_to_card`）
- §6. 提现（toC，`test_withdraw`）
- §7. 跨境汇款（toC，`test_remittance`）

## 关键方法 / 入口
queryPartnerKey

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[auto_online_business_direct_pay]](自动化:直连支付自动化)
- [[auto_online_business_pre_auth_capture]](自动化:预授权/请款自动化)
- [[scn_online_business_direct_pay]](场景:直连支付 (Direct Pay))
- [[scn_online_business_pre_auth]](场景:预授权 / 请款 (PreAuth-Capture))

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp008` · domain=`risk`。

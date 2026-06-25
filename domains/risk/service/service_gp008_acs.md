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
related_tables: []
related_scenarios: [scn_online_business_direct_pay, scn_online_business_pre_auth]
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

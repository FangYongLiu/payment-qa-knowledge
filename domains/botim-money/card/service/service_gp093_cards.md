---
id: svc_cards
object_type: Service
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp093
name: cards
dev_owner: Qian.Wang
aliases: [gp093_cards]
related_services: []
related_tables: []
related_scenarios: [scn_online_business_auto_debit, scn_online_business_cashier_pay, scn_online_business_direct_pay, scn_online_business_merchant_payout, scn_online_business_pre_auth, scn_wallet_deposit]
---

# cards

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp093` · domain=`card`。

## 作用
卡管理 —— 绑卡 / 卡 token（被收单 / 收银 / 渠道广泛调用）

## 系统中的位置
- 功能层:会员 / 账户 / 卡 / 协议 (Member / Account / Card)
- 业务域:`card`

## 关联关系

**被调用(上游)—— 这些服务调用本服务:**
merchant-frontend, tradeii, cashierii, cashdesk-api, qpay-mpgs, fundout

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）
- §2. 收银台 / 收银（`test_bpg_paypage` 收银侧、cashier 用例）
- §4. 卡渠道入金 3DS（`test_mpgs_fundIn` / `test_cko_fundIn`）
- §5. 银行/卡转账、出款（`test_transfer_to_bank` / `test_transfer_to_card`）
- §9. 登录 / KYC / 绑卡（basic_cases：`test_login` / `test_*eid*` / `test_bankcards`）

## 涉及的 API / 数据库表
- **暴露 API**(Dubbo,来源 `cards-dubbo-api` 文档):卡管理 + 地理/银行字典。核心 `CardBinFacade`(`validate`(卡 BIN 校验,收单/风控高频)/`validateCountry`/`create`/`importFile`/`queryByBinId`)、`IbanFacade`(`validateIban`/`buildIban`/`validateSwiftCode`);字典类 `BankFacade`/`BranchFacade`/`CountryFacade`/`CityFacade`/`StateFacade`/`AreaFacade`(queryByCondition/queryByCode/update)、`ImportFileFacade`。
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[auto_online_business_auto_debit]](自动化:自动代扣自动化)
- [[auto_online_business_bpg_paypage]](自动化:收银台 BPG PayPage 自动化)
- [[auto_online_business_direct_pay]](自动化:直连支付自动化)
- [[auto_online_business_dynqr]](自动化:动态二维码收银自动化)
- [[auto_online_business_pre_auth_capture]](自动化:预授权/请款自动化)
- [[auto_online_business_qr_pay]](自动化:二维码/付款码开关自动化)
- [[auto_online_business_send_pay_link]](自动化:发送支付链接自动化)
- [[auto_online_business_smart_code]](自动化:智慧码支付自动化)
- [[auto_online_business_smart_pos]](自动化:智能 POS 自动化)
- [[auto_online_business_taxi]](自动化:出租车支付自动化)
- [[auto_online_business_transfer_order]](自动化:转账下单自动化)
- [[auto_online_business_transfer_to_bank]](自动化:转账到银行自动化)
- [[auto_online_business_transfer_to_card]](自动化:转账到卡自动化)
- [[auto_wallet_deposit]](自动化:钱包充值自动化)
- [[scn_online_business_auto_debit]](场景:自动代扣 / 签约 (Auto Debit))
- [[scn_online_business_cashier_pay]](场景:收银台支付 (Cashier / PayPage))
- [[scn_online_business_direct_pay]](场景:直连支付 (Direct Pay))
- [[scn_online_business_merchant_payout]](场景:商户出款 / 转账 (Transfer / Payout))
- [[scn_online_business_pre_auth]](场景:预授权 / 请款 (PreAuth-Capture))
- [[scn_wallet_deposit]](场景:钱包充值 (Deposit / Top-Up))

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp093` · domain=`card`。

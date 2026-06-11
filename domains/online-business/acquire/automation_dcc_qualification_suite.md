---
id: auto_dcc_qualification_suite
object_type: AutomationAsset
name: "DCC via CKO 集成自动化套件"
aliases: ["DCC自动化", "DCC自动化套件", "DCC automation suite", "dcc qualification suite"]
domain: online-business
subdomain: acquire
module: DCC
status: active
owner: QA-Team
reviewer: QA-Team
last_reviewed_at: 2026-05-20
source_type: testcase
source_ref: "DCC_Via_CKO Integration Test Cases (E2E / Availability / Quotation / Refund)"
tags: ["automation", "DCC", "CKO"]
related_services: ["svc_acquireii"]
related_scenarios: ["scn_dcc_accepted", "scn_dcc_declined", "scn_dcc_not_eligible"]
---

## 用途
覆盖 DCC via CKO 的集成回归:报价、资格判定、Accept/Decline/NotEligible、创建订单校验(过期/不匹配/篡改/未授权)、退款(全额/部分/末笔)与取消。

## 覆盖场景
- `scn_dcc_accepted`、`scn_dcc_declined`、`scn_dcc_not_eligible`
- 报价字段与精度(USD/JPY/KWD/BHD);Create Order 拒绝类用例。

## 运行方式
- 集成环境跑用例集;依赖测试商户已开通 DCC、provider=CKO、可用测试卡(如 4273149019799094)、Metadata/FX 可用。

## 常见失败原因
- 测试商户 DCC 资质被重置 / provider 配置变更;卡 BIN/币种数据失效;报价过期(15min)导致下单失败;Metadata/FX 环境不稳定。

## 维护者
- QA-Team(对照覆盖场景定位失败)。

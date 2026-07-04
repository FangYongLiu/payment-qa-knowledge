---
id: svc_dpm_manager
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp004
name: dpm-manager
dev_owner: Cong.Zhou
aliases: [gp004_dpm-manager]
related_services: []
related_tables: []
---

# dpm-manager

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp004` · domain=`payment-core`。

## 作用
账务平台管理（DPM）—— 记账主入口，被 pfs/payment/reconciliation 调用

## 系统中的位置
- 功能层:出款 / 账务 / 对账 (Fundout / Accounting / Recon)
- 业务域:`payment-core`

## 关联关系

**被调用(上游)—— 这些服务调用本服务:**
pfs-payment, reconciliation, payment

## 参与的业务场景(cgs 回归)
- §1. 直连支付 / 预授权 / DCC（toB，`test_direct_pay` / `test_pre_auth_capture` / `test_bpg_paypage`）

## 涉及的 API / 数据库表
- **暴露 API**(Dubbo,来源 `dpm-manager-dubbo-api` 文档):`AccountService`(账户主数据:`getAccountByAccountNo` / `getAccountDetailList` / `insertOuterAccount` / `insertInnerAccount` / `createAccountTitle` / `queryInnerAccounts` / `changeActivatedAccountStatus` / `queryStatusChangeHis` 等)、`BufferRuleService.insertBufferRule`、`TitleDailyQueryFacade.queryTitleDaily`。被 [[svc_pfs_payment]]/[[svc_payment]]/[[svc_reconciliation]]/[[svc_member]] 调。
- **读写的表**:`T_DPM_ACCOUNT_CRL_DEF`(账户控制/余额定义)等 DPM 账户表(具体对象待补)。

## 关键方法 / 入口(UAT 实测)
- `[APP-->DPMV2]获取账户信息请求:accountNo=<784…>` → `开始查询 T_DPM_ACCOUNT_CRL_DEF 表` → 返回账户信息;[[svc_member]] 查账户时 `路由到 dpmAccountClient` 命中本服务。
- 账户号格式:`784200100…`(DPM V2 账户号)。

## 测试要点 / 排障 / 常见问题(UAT 实测)
- **职责边界**:dpm-manager = 账户**主数据/查询**(账户存在性、余额定义);[[svc_dpm_accounting]] = **入账**(改余额)。定位余额问题先分清"查不到账户(manager)"vs"入账未更新(accounting)"。
- **怎么测/定位**:按 `accountNo`(784…)查 `T_DPM_ACCOUNT_CRL_DEF`;member→dpm 路由(`dpmAccountClient`)是否命中。
- 账务链:[[svc_member]](账户门面)→ dpm-manager(账户主数据)→ [[svc_dpm_accounting]](入账)。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[flow_cashier_payment]](流程:收银台 / 收单卡支付端到端流程（含退款）)

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp004` · domain=`payment-core`。

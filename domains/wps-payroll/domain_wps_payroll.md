---
id: domain_wps_payroll
object_type: Domain
domain: wps-payroll
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: confluence:AQ/2272428082
tags:
- payroll
- UAE
- wps
subdomain: null
module: null
sensitivity: normal
name: WPS薪资保障业务域
aliases:
- Wage Protection System
- WPS
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
WPS (Wage Protection System) 是面向 UAE 的薪资发放平台。企业 (corporate) 在该平台完成入驻、员工注册并发放薪资，发放渠道有两种：
- 通过 UAE 央行 (CBUAE) 的 WPS 文件交换系统 (SIF/PIF/PRC/DIF)
- 通过 Direct Transfer 直接转账

通过 Botim Wallet 收薪的员工会获得实体 Botim Payroll Card，并在 Botim App 中完成激活。

知识库分为两部分：
- WPS System — Knowledge Base：企业侧端到端产品流程（公司注册、发票/计费配置、添加员工、创建 payroll、WPS portal、PAF 类型公司）
- Botim Payroll Card — Activation & Card Management：员工侧卡片生命周期（发卡、激活、QR/CVV/proxy 获取、YSE 卡状态协同、替换、关闭）

## 覆盖范围
本域涵盖以下整体业务流：

1. **Company onboarding**：企业在 merchant portal 注册，启用 WPS 服务，选择公司类型 (WPS-Mainland / Listed LRAs / Non-Listed LRAs / PDC)，由 Basis 审核后注册到 YSE 并获得 IBAN。
2. **Billing setup**：在执行计费操作之前，由 staff 在 Basis 配置 invoice 模型 (Pay Now 或 Pay Monthly)。
3. **Add employee**：员工以 EID 或 Passport 注册，作为 Botim Wallet 或 Bank Account 用户，在 Basis 审核后通过 CSPREG 同步至 YSE；Botim Wallet 员工通过 YSE-WPSCSR 发卡。
4. **Card issuance → activation**：员工收到带 QR code 的 Botim Payroll Card，在 Botim App 完成 KYC，YSE 将卡置为 activatable 状态，员工激活（EID 通过按钮或 QR；Passport 必须走 QR + Passport KYC）。
5. **Create payroll**：通过 WPS（央行文件交换 SIF/PIF/PRC/DIF）或 Direct Transfer 发放薪资，由 portal 审批并经 YSE/TradeII 执行。
6. **Ongoing management**：企业通过 WPS portal 自助管理 (Dashboard / Payrolls / Employees / Invoice / Reports / Roles)；员工自助管理卡 (replace / statement / close)。

## 关键服务/流程
- **YSE**：第三方合作方，生成/上传央行文件并暴露 API (CSPREG, WPSCSR, WPSSAL, BPSLS 等)；所有 YSE 调用经由 PPC 路由；YSE 也负责 card state (activatable / suspended / closed)。
- **PPC**：内部转发服务，所有 YSE 调用通过它中转；`ppc.t_virtual_card` 是卡管理的虚拟卡数据存储。
- **CBUAE**：UAE 央行，文件交换模型中的 WPS 节点；只通过我方 SFTP 与 CBUAE 交换文件，YSE 不直连央行。
- **TradeII**：内部交易服务，执行资金划转（如 company pool → Payby pool）。
- **Basis**：内部员工平台，用于商户/员工审核、invoice 配置、加解密（如解密 card CVV）。

两个关键差异：
- **SIF vs PAF**（`bps.t_corporate.process_type`）：SIF 是默认端到端产品（portal 发放、invoice 模块）；PAF 仅作为发放通道——无 portal 发放、无 invoice 模块、线下结算、YSE 驱动发放，存在 parent/sub-company 结构。
- **EID vs Passport 员工**：Passport 用户始终是 Botim 卡用户，初始状态为 KYCVerification，必须走 QR-code 路径在卡激活时进入 Passport KYC；EID 用户可通过按钮或 QR 激活。

## QA 关注点
- 公司类型分支：WPS-Mainland / Listed LRAs / Non-Listed LRAs / PDC，以及 SIF vs PAF 的差异化流程（PAF 不走 portal、无 invoice、parent/sub 结构）。
- 员工注册路径：EID vs Passport、Botim Wallet vs Bank Account；Passport 用户必须 QR + KYCVerification。
- YSE API 同步链路：CSPREG（员工注册）、WPSCSR（发卡）、WPSSAL/BPSLS（薪资）的 PPC 转发与状态回写。
- 央行文件交换：SIF/PIF/PRC/DIF（发放）与 EIF/WIF（Non-Listed LRAs，存于 `t_esa_file_record`/`_detail`），仅经 SFTP。
- 卡生命周期与 KYC 闭环：发卡 → KYC → YSE 状态翻转 activatable → 激活；卡状态 (activatable/suspended/closed) 由 YSE 持有。
- 关键数据表分布：
  - Company：`bps.t_corporate` (+ `_profile`/`_account`/`_address`/`_mohre`)、`vis.t_virtual_account` (IBAN)
  - Invoice：`bps.t_corp_invoice_config`、`t_corp_invoice`/`_item`、`t_corp_invoice_fee_code`/`_item_code`
  - Employee：`bps.t_employee_corporate`（主表，含 status）+ `t_employee`/`_profile`/`_salary_account`/`_address`、`t_employee_kyc_material`（passport）
  - Payroll：`bps.t_payroll_source`/`_bulk`/`_data`、`t_salary_load_command`/`_execute`、`t_cb001_transfer_record`、`t_salary_load_record`；PAF：`t_payroll_paf`/`_detail`
  - Card：`ppc.t_virtual_card`（proxy/CVV/state）、`bps.t_employee_salary_account`（card_ref_mid/vid、IBAN、routing）、`bps.t_employee_profile`（qr_code）
- 关联 KYC 知识库：UAEKYC / UAE Pass / Passport，其中 Passport 通道专属 WPS-worker 路径，且为卡激活与资金交易的前置门控。

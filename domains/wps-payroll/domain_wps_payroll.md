---
id: domain_wps_payroll
object_type: Domain
domain: wps-payroll
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: wiki:71f029c9-8348-44b0-9b2c-61fc499d4ecf
tags:
- payroll
- UAE
- WPS
- BotimPayrollCard
subdomain: null
module: null
sensitivity: normal
name: WPS薪资发放业务域
aliases:
- WPS
- Wage Protection System
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
WPS (Wage Protection System) 是面向 UAE 的薪资发放平台。企业 (Corporate) 在商户端入驻、注册员工，并通过 UAE 央行 (CBUAE) 的 WPS 文件交换系统或 Direct Transfer 直接转账方式向员工发放薪资。使用 Botim Wallet 收薪的员工会收到一张实体 Botim Payroll Card，并在 Botim App 中完成激活。

业务域知识库拆为两份文档：
- **WPS System — Knowledge Base**：覆盖企业侧端到端的薪资产品(公司注册、invoice/billing 配置、添加员工、创建 payroll(WPS & Direct Transfer)、WPS portal、PAF 类公司)。
- **Botim Payroll Card — Activation & Card Management**：覆盖员工侧的薪资卡生命周期(发卡、激活(EID vs Passport)、QR/CVV/proxy 获取、YSE 卡状态协同、replace、close)。

## 覆盖范围
本业务域覆盖以下完整链路：
1. **Company onboarding**：企业在 merchant portal 注册，开通 WPS 服务，选择公司类型 (WPS-Mainland / Listed LRAs / Non-Listed LRAs / PDC)，由 Basis 审核，注册到 YSE，获得 IBAN。
2. **Billing setup**：在收费操作前，由 staff 在 Basis 配置 invoice 模型 (Pay Now 或 Pay Monthly)。
3. **Add employee**：通过 EID 或 Passport 注册员工，类型为 Botim Wallet 或 Bank Account，Basis 审核后通过 CSPREG 同步至 YSE；Botim wallet 员工通过 YSE-WPSCSR 发卡。
4. **Card issuance → activation**：发出的 Botim Payroll Card 带有印刷 QR code，员工在 Botim App 完成 KYC，YSE 将卡切换至 activatable 状态，员工激活 (EID：按钮或 QR；Passport：QR + Passport KYC)。
5. **Create payroll**：通过 WPS (央行文件交换：SIF/PIF/PRC/DIF) 或 Direct Transfer 发薪，portal 审批后由 YSE/TradeII 执行。
6. **Ongoing management**：企业通过 WPS portal 自助管理 (Dashboard, Payrolls, Employees, Invoice, Reports, Roles)；员工管理卡片 (replace, statement, close)。

两个重要变体：
- **SIF vs PAF** (`process_type` 字段位于 `bps.t_corporate`)：SIF 为默认端到端产品；PAF 仅作为发薪通道，无 portal disbursement、无 invoice module、离线结算、YSE 驱动发薪、有 parent/sub-company 结构。
- **EID vs Passport employees**：Passport 用户必为 Botim-card 用户，初始状态 KYCVerification，必须走 QR-code 路径触发 Passport KYC；EID 用户可走按钮或 QR。

## 关键服务/流程
**关键参与方 (Actors)**：
- **YSE**：第三方合作方，生成/上传央行文件，暴露 CSPREG、WPSCSR、WPSSAL、BPSLS 等 API；所有 YSE 调用经 PPC 转发；同时持有卡状态 (activatable / suspended / closed)。
- **PPC**：内部转发服务，负责所有 YSE 交互；`ppc.t_virtual_card` 为虚拟卡数据存储。
- **CBUAE**：UAE 央行，文件交换模型中的 WPS 节点；文件仅通过我方 SFTP 与 CBUAE 交换，YSE 不直接对接央行。
- **TradeII**：内部交易服务，执行资金划转 (如 company pool → Payby pool)。
- **Basis**：内部员工平台，用于商户/员工审核、invoice 配置、加解密 (如解密 card CVV)。

**数据落点 (quick map)**：
- Company：`bps.t_corporate` (+ `_profile` / `_account` / `_address` / `_mohre`)、`vis.t_virtual_account` (IBAN)
- Invoice / billing：`bps.t_corp_invoice_config`、`t_corp_invoice` / `_item`、`t_corp_invoice_fee_code` / `_item_code`
- Employee：`bps.t_employee_corporate` (主表，含 status) + `t_employee` / `_profile` / `_salary_account` / `_address`；`t_employee_kyc_material` (passport)
- Payroll：`bps.t_payroll_source` / `_bulk` / `_data`、`t_salary_load_command` / `_execute`、`t_cb001_transfer_record`、`t_salary_load_record`；PAF：`t_payroll_paf` / `_detail`
- 央行文件：`t_esa_file_record` / `_detail` (EIF/WIF for Non-Listed LRAs)
- Card：`ppc.t_virtual_card` (proxy/CVV/state)、`bps.t_employee_salary_account` (card_ref_mid/vid, IBAN, routing)、`bps.t_employee_profile` (qr_code)

## QA 关注点
- 区分 **SIF vs PAF**：通过 `bps.t_corporate.process_type` 判断公司类型；PAF 没有 portal disbursement 与 invoice module，不要按 SIF 流程验证。
- 区分 **EID vs Passport** 员工激活路径：Passport 用户只能走 QR-code 路径触发 Passport KYC，且强制为 Botim-card 用户。
- 所有 YSE 接口 (CSPREG、WPSCSR、WPSSAL、BPSLS) 调用必经 PPC，排查时优先看 PPC 转发日志。
- CBUAE 文件交换仅经我方 SFTP，YSE 不直连央行；文件类型 SIF/PIF/PRC/DIF (发薪) 与 EIF/WIF (Non-Listed LRAs，落 `t_esa_file_record`/`_detail`) 不要混淆。
- 卡状态由 YSE 持有 (activatable / suspended / closed)，本地 `ppc.t_virtual_card` 状态需与 YSE 协同。
- KYC 属独立知识库 (UAEKYC / UAE Pass / Passport)，但 Passport 通道专为 WPS-worker 设计，是卡激活与资金交易的前置门控。

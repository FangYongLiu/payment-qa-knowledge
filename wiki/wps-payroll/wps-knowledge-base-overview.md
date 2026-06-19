---
title: WPS知识库总览
domain: wps-payroll
kind: wiki_page
slug: wps-knowledge-base-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:71f029c9-8348-44b0-9b2c-61fc499d4ecf
tags: []
---

# WPS知识库总览

WPS（Wage Protection System）是面向阿联酋的薪资发放产品，本页作为入口，帮助新人快速了解产品定位、关键参与方、端到端旅程以及数据存储分布。业务域归属 [[domain_wps_payroll]]。

## 产品定位

- **WPS（Wage Protection System）**：阿联酋薪资发放平台。
- 企业（Corporate）在平台上完成入驻、员工注册、薪资发放。
- 发放方式两种：
  - 通过阿联酋央行 **CBUAE** 的 WPS 文件交换通道
  - **Direct Transfer**（直接转账）
- 通过 **Botim Wallet** 收薪的员工，会收到实体 **Botim Payroll Card**，并在 Botim App 中激活。

## 知识库划分

知识库分为两份文档：

| 文档 | 覆盖范围 | 何时阅读 |
|---|---|---|
| WPS System — Knowledge Base | 公司侧端到端：公司注册、Invoice/Billing 配置、员工添加、创建 Payroll（WPS 与 Direct Transfer）、WPS Portal、PAF 类型公司 | 需要查公司入驻、员工注册、发放流程、DB 表与状态、YSE/央行文件交换 |
| Botim Payroll Card — Activation & Card Management | 员工侧卡片生命周期：发卡、激活（EID vs Passport）、QR/CVV/proxy 获取、YSE 卡状态协调、换卡、销卡 | 需要查员工在 Botim App 中如何激活/管理薪资卡，或排查卡数据与状态 |

## 关键参与方

| 角色 | 职责 |
|---|---|
| **YSE** | 第三方合作方。生成并上传央行文件，提供 CSPREG、WPSCSR、WPSSAL、BPSLS 等 API；所有 YSE 调用都经 PPC 路由。同时持有卡状态（activatable / suspended / closed）。 |
| **PPC** | 内部转发服务，承载所有 YSE 交互（"调用 YSE API" = "通过 PPC 调用"）。`ppc.t_virtual_card` 为卡管理使用的虚拟卡数据存储。 |
| **CBUAE** | 阿联酋央行，文件交换模型中的 WPS 节点。文件仅通过我方 SFTP 与 CBUAE 交换，YSE 不直接对接央行。 |
| **TradeII** | 内部交易服务，执行资金划拨（如 company pool → Payby pool）。 |
| **Basis** | 内部员工后台，用于商户/员工审核、Invoice 配置、加解密（如解密卡 CVV）。 |

## 端到端旅程（两份文档如何串联）

1. **Company onboarding**：商户在 merchant portal 注册，开通 WPS 服务，选择公司类型（WPS-Mainland / Listed LRAs / Non-Listed LRAs / PDC），由 Basis 审核，向 YSE 注册，获得 IBAN。（WPS System §2）
2. **Billing setup**：在产生计费操作前，Staff 在 Basis 配置 Invoice 模型（**Pay Now** 或 **Pay Monthly**）。（WPS System §3）
3. **Add employee**：员工以 **EID** 或 **Passport** 注册，类型为 **Botim Wallet** 或 **Bank Account**，经 Basis 审核，通过 CSPREG 同步至 YSE；Botim Wallet 用户再通过 YSE-WPSCSR 发卡。（WPS System §4）
4. **Card issuance → activation**：发出的 Botim Payroll Card 印有 QR code；员工在 Botim App 完成 KYC，YSE 把卡置为 activatable，员工激活（EID：按钮或 QR；Passport：QR + Passport KYC）。（Payroll Card §2–§6；KYC 本身归独立的 KYC 知识库 — UAEKYC / UAE Pass / Passport）
5. **Create payroll**：公司通过 **WPS**（央行文件交换：SIF/PIF/PRC/DIF）或 **Direct Transfer** 发薪，在 portal 审批后通过 YSE/TradeII 执行。（WPS System §5）
6. **Ongoing management**：公司在 WPS portal 自助管理（Dashboard、Payrolls、Employees、Invoice、Reports、Roles）；员工管理卡片（replace、statement、close）。（WPS System §6，Payroll Card §7–§8）

## 两个需要分清的变体

### SIF vs PAF

由 `bps.t_corporate` 中的 `process_type` 决定：

- **SIF**：默认端到端产品，含 portal 发放、Invoice 模块。
- **PAF**：仅作为发放通道——无 portal 发放、无 Invoice 模块、线下结算、由 YSE 驱动发放、存在 parent/sub-company 结构。

详见 WPS System §7。

### EID vs Passport 员工

- **Passport** 用户：始终为 Botim-card 用户，初始状态 `KYCVerification`，必须走 **QR-code** 路径才能在卡片激活时进入 Passport KYC 选项。
- **EID** 用户：可通过按钮或 QR 激活。

详见 WPS System §4.7、Payroll Card §2。

## 数据存储快速映射

| 领域 | 主要表 |
|---|---|
| Company | `bps.t_corporate`（含 `_profile` / `_account` / `_address` / `_mohre`），`vis.t_virtual_account`（IBAN） |
| Invoice / billing | `bps.t_corp_invoice_config`，`t_corp_invoice` / `_item`，`t_corp_invoice_fee_code` / `_item_code` |
| Employee | `bps.t_employee_corporate`（主表，持有状态）+ `t_employee` / `_profile` / `_salary_account` / `_address`；`t_employee_kyc_material`（passport） |
| Payroll | `bps.t_payroll_source` / `_bulk` / `_data`，`t_salary_load_command` / `_execute`，`t_cb001_transfer_record`，`t_salary_load_record`；PAF：`t_payroll_paf` / `_detail` |
| Central-bank files | `t_esa_file_record` / `_detail`（EIF/WIF，用于 Non-Listed LRAs） |
| Card | `ppc.t_virtual_card`（proxy/CVV/state），`bps.t_employee_salary_account`（card_ref_mid/vid、IBAN、routing），`bps.t_employee_profile`（qr_code） |

## 相关知识库

- **KYC — Channel Overview**（UAEKYC / UAE Pass / Passport）：身份验证步骤，决定卡片激活与资金交易的开通；其中 **Passport** 通道专用于 WPS-worker 路径。

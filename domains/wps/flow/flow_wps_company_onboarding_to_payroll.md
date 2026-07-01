---
id: flow_wps_company_onboarding_to_payroll
object_type: Flow
name: WPS 企业入驻到发薪端到端流程
aliases: [WPS company onboarding to payroll, WPS 薪资发放全流程]
domain: wps
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/2272428082
tags: [wps, payroll, onboarding, UAE]
related_services: [svc_payroll_core_service, svc_ppc, svc_tradeii]
related_tables: [tbl_bps_t_corporate, tbl_bps_t_employee_corporate, tbl_bps_t_payroll_source, tbl_ppc_t_virtual_card]
related_scenarios: [scn_wps_sif_vs_paf]
---

# WPS 企业入驻到发薪端到端流程

## 概述
WPS(Wage Protection System)是面向阿联酋(UAE)的薪资发放平台。本流程串起企业从在商户门户入驻、配置计费、登记员工、员工激活 Botim Payroll Card,到最终发放薪资的完整端到端旅程。终点是薪资经央行文件交换(SIF/PIF/PRC/DIF)或 Direct Transfer 落到员工账户/卡。

发放路径有两种:
- 经阿联酋央行(CBUAE)的 WPS 文件交换体系(SIF/PIF/PRC/DIF);
- Direct Transfer 直接转账。

通过 Botim Wallet 发薪的员工会收到一张实体 Botim Payroll Card,并在 Botim App 内激活。

## 步骤(跨系统)
1. **Company onboarding** —— 企业在商户门户注册,开通 WPS 服务,选择公司类型(WPS-Mainland / Listed LRAs / Non-Listed LRAs / PDC);由 Basis(运营平台)审核通过,注册到 YSE 并获得 IBAN。落库 [[tbl_bps_t_corporate]](+ `_profile`/`_account`/`_address`/`_mohre`)、`vis.t_virtual_account`(IBAN,待补对象)。
2. **Billing setup** —— 任何计费操作前,由 staff 在 Basis 配置 invoice 模式(`Pay Now` 或 `Pay Monthly`)。落库 `bps.t_corp_invoice_config` 等(待补对象)。
3. **Add employee** —— 以 EID 或 Passport 登记员工,类型为 Botim Wallet 或 Bank Account;Basis 审核后通过 YSE-CSPREG 同步到 YSE;Botim Wallet 员工随后通过 YSE-WPSCSR 发卡。落库 [[tbl_bps_t_employee_corporate]](主表,含 status)+ `t_employee`/`_profile`/`_salary_account`/`_address`、`t_employee_kyc_material`(护照 KYC 资料)。
4. **Card issuance → activation** —— 卡片到达后带印刷 QR 码;员工在 Botim App 完成 KYC,YSE 将卡置为 activatable 状态,员工激活(EID:按钮或 QR;Passport:必须走 QR + Passport KYC)。卡状态/proxy/CVV 落 [[tbl_ppc_t_virtual_card]]。所有 YSE 调用经 [[svc_ppc]] 转发。
5. **Create payroll** —— 经 WPS(央行文件交换 SIF/PIF/PRC/DIF)或 Direct Transfer 发薪;门户审批后由 YSE/[[svc_tradeii]] 执行资金划转(如 company pool → Payby pool)。落库 [[tbl_bps_t_payroll_source]](+ `_bulk`/`_data`)、`t_salary_load_command`/`_execute`、`t_cb001_transfer_record`、`t_salary_load_record`。
6. **Ongoing management** —— 企业经 WPS 门户自助管理(Dashboard / Payrolls / Employees / Invoice / Reports / Roles);员工自助管理卡(replace / statement / close)。

## 关联关系
- **经过的服务(有序)**:[[svc_payroll_core_service]] → [[svc_ppc]](统一转发到 YSE)→ [[svc_tradeii]](资金划转)(= `related_services`)。外部参与方 YSE / CBUAE 为第三方/央行,未建服务对象(见下「参与方」)。
- **关键表**:[[tbl_bps_t_corporate]] / [[tbl_bps_t_employee_corporate]] / [[tbl_bps_t_payroll_source]] / [[tbl_ppc_t_virtual_card]](= `related_tables`)。
- **关键场景**:[[scn_wps_sif_vs_paf]](= `related_scenarios`)。

## 参与方(外部 / 未建服务对象,待补)
- **YSE**:第三方合作方,WPS 对外核心通道;生成/上传央行文件,暴露 API(CSPREG 员工注册 / WPSCSR 发卡 / WPSSAL / BPSLS 薪资等);持有卡状态(activatable / suspended / closed)。所有对 YSE 的调用一律经 [[svc_ppc]] 转发,YSE 不直连央行。(YSE 为外部合作方,未建 svc 对象,标「待补」)
- **CBUAE(UAE 央行)**:文件交换模型中的 WPS 节点;与 CBUAE 的文件交换只走我方自有 SFTP 通道。(外部,未建对象)
- **Basis**:内部运营/员工平台,负责商户/员工审核、invoice 配置、加解密(如解密卡 CVV)。Basis 相关服务对象见 portal-operations 域(`svc_basis` 等),与本 WPS 流程的精确映射「待补」。

## 校验点
- 公司类型分支正确落库 `bps.t_corporate.process_type`(SIF / PAF),分支行为见 [[scn_wps_sif_vs_paf]]。
- 员工注册路径:EID vs Passport、Botim Wallet vs Bank Account;Passport 用户初始状态 `KYCVerification`,卡激活时必须走 QR-code 路径才能进入 Passport KYC。
- YSE 同步链路状态回写:CSPREG(员工注册)、WPSCSR(发卡)、WPSSAL/BPSLS(薪资)经 PPC 转发后,状态是否正确回写应用侧。
- 央行文件交换:SIF/PIF/PRC/DIF(发放)与 EIF/WIF(Non-Listed LRAs,存 `bps.t_esa_file_record`/`_detail`)仅经 SFTP。
- 卡生命周期闭环:发卡 → KYC → YSE 状态翻转 activatable → 激活,卡状态由 YSE 持有并经 PPC 同步落 `ppc.t_virtual_card`。
- 关联 KYC 前置:UAEKYC / UAE Pass / Passport 通道,其中 Passport 通道专属 WPS-worker 路径,是卡激活与资金交易的前置门控(KYC 域细节待补)。

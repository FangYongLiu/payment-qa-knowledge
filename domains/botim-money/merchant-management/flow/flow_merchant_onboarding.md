---
id: flow_merchant_onboarding
object_type: Flow
name: 商户注册与入驻端到端流程(Acquire + WPS)
aliases: [merchant onboarding, 商户入驻, merchant register acquire, merchant open wps]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-05'
source_type: wiki
source_ref: 'confluence:AQ/997785804, AQ/997818451, tester/462749700, wiki:34ef57ae + 商户端系2025(注册核身细节)'
tags: [merchant, onboarding, acquire, wps, kyb, aml, 核身]
related_services: [svc_unified_merchant_portal, svc_merchant, svc_member, svc_basis_merchant, svc_aml, svc_vis, svc_ppcenter, svc_contract, svc_statementii, svc_grc_check_identity_provider, svc_cgs, svc_cmsii, svc_otps, svc_mns_scheduler]
related_tables: [tbl_member_tm_member, tbl_member_tm_member_identity, tbl_member_tr_beneficiary_info, tbl_member_tr_member_account]
related_scenarios: [scn_merchant_portal_registration]
---

# 商户注册与入驻端到端流程(Acquire + WPS)

## 概述
商户从 Unified Portal 首次注册/登录，提交入驻资料并选择业务类型(Payment=Acquire / WPS)，经 BMOC(Basis Merchant)后台完成 AML 风险计算与 KYB 审核后激活。入驻是跨系统流程，涉及 Member、Merchant、Basis、AML、VIS、Billing、Contract 多个服务，**任一环节失败都会阻塞商户激活**，所有相关库表均有记录后商户才视为可用。

起点:Unified Portal 注册 → 终点:商户激活、可使用收单/发薪能力。

## 步骤(跨系统)
1. **注册/登录(含风控核身)** —— [[svc_unified_merchant_portal]] / 控台前端:首次默认 OTP 登录(Sim 固定 `161616`，UAT 需真实 OTP)，登录后必须设置密码;管理员手机号即后续登录账号(administrator role)。
   门户自助注册的**前端申请人视角**完整向导(Pricing→Company Profile→Business Information→Management→Review→DocuSign→Submitted,含每步字段/上传/子问卷)见 [[scn_merchant_portal_registration]]。
   **核身细节(新手机号注册,来源 商户端2025)**:`login/smsCode/preSubmit` 提交手机号 → 控台前端 → [[svc_member]] 按手机号查会员,不存在则走注册 + `otherEventFacade.riskOtherEvent` 请求 [[svc_grc_check_identity_provider]] 风控;核身开关开时返回 `{PRE=CAPTCHA, INTERNAL=OTP}`。核身 API 经 [[svc_cgs]]:`/api/cgs/risk-identify/v1/unauth/refresh-captcha → verify-captcha → send-identity-otp → verify-identity-otp`;链路 cgs→grc 验 CAPTCHA、grc→[[svc_cmsii]] 查白名单、grc→member 取 partnerId、grc→[[svc_otps]] 发 OTP、otps→[[svc_mns_scheduler]]→MQ 发短信、grc 验 OTP `result=pass`。注册提交:`/api/acquiring/preAuth/register/generateSalt → /submit`;成功后 [[svc_member]] 设置支付密码 `payPwd`。
2. **提交 Acquire 申请** —— 接口 [[api_merchant_apply_add]] `/api/acquiring/permitAll/merchant/apply/add`，可选 `Acquire` 或 `WPS`。请求体字段:`acquireInfoList / addressList / bindingCard / bizAdminList / merchantData / partnerList / signatory / wpsInfoList`。入驻表单含公司基础信息与银行账户/IBAN(测试值 `AE790030013112189920001`，后端校验)。此阶段 Merchant 库写入初始数据，Member 库会员处于**未激活**(状态 0)。
3. **BMOC 审核(两步:AML 风险计算 → KYB 审批)** —— [[svc_basis_merchant]]。BMOC 登录 LDAP 员工域账号(basis-cas),菜单 `Basis Merchant => BUSINESS => Merchant => **Merchant Onboarding**`(⚠️ 是 `Merchant Onboarding`,**不是** `Merchant Onboarding Management`=渠道报备/Fund Provider;也区别于单步的 `Merchant Approval`)。
   列表列:Apply ID / Source(PORTAL/BASIS/AGENT)/ Merchant ID / Merchant Name / Business / Signatory / Service(ACQUIRE/WPS)/ Application 日期 / **Application Status**(`Awaiting Approval`→`Approved`)/ **Compliance**(风险等级)/ **Compliance**(KYB 状态,如 `Awaiting KYB`)/ Action。待审行操作:`View / AML Risk Calc / KYB Approval / Reject`。**必须先 AML Risk Calc,再 KYB Approval**。
   - **① AML Risk Calc**(点开 `Risk Calculate` 表单,是风险打分):
     - *Merchant Information*:Whether Internal、Business Name、Category(MCC)、Business Type、Legal Type、Tax Registration Number、Screening result(文件)、Compliance Level、Botim Business Type、Company Logo。
     - *Compliance Risk Assessment*:High-Risk Jurisdiction Involvement、Monthly Turnover、Payment Methods、Delivery Channels(多为申请带出)。
     - *Compliance Risk Calculate Information*(各为风险因子,均必填下拉):`Industry Type`、`Sanctions Screening`(no hit / immaterial / material-need escalation)、`ADV PEP Screening`(no hit / PEP·Adverse news × immaterial·material)、`UBO Nationality`(国家,可搜索)、`Business Profile Overview`(经营年限/资本)、`Product Services`(ISIC 类,可搜索)。
     - *Other*:Agent Information(Agent Merchant Mid / Mobile / Merchant Contract 文件)、Referrer Information(Referrer Merchant Mid)——选填。
     - 底部 **`Save & Calculate`** → 二次确认 `Confirm` → 计算出 **Onboarding Risk Assessment**(Low/Medium/High)+ **Onboarding Risk Score**(实测 `Medium` / `6.51`)。此步完成后该行 KYB 状态 = `Awaiting KYB`。AML 失败/高风险会阻断([[svc_aml]])。
     - ⚠️ 网关会话较短,长表单期间可能超时踢回 basis-cas 登录页;`Save & Calculate` 的结果已服务端持久化,重登后可直接接 KYB。
   - **② KYB Approval**(AML 完成后点开):表单极简 —— `Result`(**PASS**/REJECT)+ `*Reason`(审核意见)→ `Confirm`。
   - **`Confirm` 后 Application Status → `Approved`,商户激活**(实测 Apply ID 2466 ACQUIRE:AML=Medium/6.51 → KYB PASS → Approved)。已批准行操作变为 `View`(WPS/其它已批行为 `View` 或 `MCC Confirm`)。
   - 其它相关菜单(同 `Merchant` 下):`Merchant Approval`(另一条单步审批入口)、`Merchant Onboarding Management`(渠道报备/Fund Provider,≠此处 KYB)、`Merchant Management`、`Application Approval`、`Tax Info Approval`、`Bank Account Approval`、`Common Approval`、`Merchant Compliance Audit Log`(审计日志)等。
4. **Acquire 审核通过** —— 激活商户与会员(状态 0→1)，联动 [[svc_ppcenter]](产品申请/订单 Merchant VAM Topup)、会员账户(BASIC)、受益人卡、[[svc_statementii]] 对账单配置、[[svc_contract]] 合同。
5. **(可选)申请开通 WPS** —— 接口 [[api_merchant_bizopen_wps]] `api/acquiring/secure/merchant2/bizOpen/wps`(请求体 `bizAdminList / wpsInfoList`)，先落 `t_common_audit_order` 公共审核;Basis 审核通过后写 WPS 业务信息、`WPS_SALARY` 账户，[[svc_vis]] 创建虚拟账户(Status: Initial)。**UAT 环境 Iban 需手动推进**。

## 渠道报备 / 入网(可收款前提,与本流程衔接)
商户/门店/设备激活后,需向收单机构渠道**报备(onboarding)**才能收款:自动报备见 [[svc_cregister]] `cregister.t_register_order`(`request_type=MCR`;`register_type` MERCHANT/STORE/DEVICE;`inst_code`+`fund_channel_code`)→ `t_register_result`;MPGS 等**人工报备**见 [[flow_mpgs_manual_onboarding]] / [[scn_onboarding_manual_register]]([[svc_onboarding]])。设备激活见 [[reference_device_activation_overview]]。

## 关联关系
- **经过的服务(有序)**:[[svc_unified_merchant_portal]] → [[svc_merchant]] → [[svc_member]] → [[svc_basis_merchant]] → [[svc_aml]] → [[svc_ppcenter]] → [[svc_vis]] → [[svc_contract]] → [[svc_statementii]](= `related_services`)
- **注册核身**:[[svc_cgs]] / [[svc_grc_check_identity_provider]] / [[svc_otps]] / [[svc_mns_scheduler]] / [[svc_cmsii]](CAPTCHA/OTP,见步骤 1)。
- **关键表**:商户主库 `merchant`(含 t_merchant / t_merchant_creation_order 等,见 `merchant-management/table/merchant/`)
- **入驻涉及接口**:[[api_merchant_apply_add]]、[[api_merchant_bizopen_wps]]
- **环境与后台入口**:见 [[reference_portal_env_access]]、[[reference_bmoc_basis_merchant]]

## 实测服务调用链(UAT Kibana,2026-07)
> 来源:UAT `java-kafka-logstash-*` 日志,按 `*ClientImpl` 聚合 + 按商户号/税号/ApplyId(如税号 `100123456700003`、ApplyId `2466`)时间线还原。`*ClientImpl` 的类名词根即被调服务。

**① 门户提交(前端 → 落申请单)**
- `merchant-console-frontend`(BFF/控台后端)接收 Portal 提交:`UnifyReceiveAccessServiceImpl` / `DefaultUnifyClient` / `LogCallTemplateAspect` / `OperateLogAspect`;下游 `Ues2ClientImpl`(会员/权限)、`DefaultResourceClientImpl`、`MqSenderClientImpl`(发 MQ)。
- 写入商户申请单(`t_merchant_creation_order`),WPS 侧 `payroll-core-service.PortalServiceFacadeImpl` 参与;此阶段会员未激活。

**② 注册核身(新手机号,见步骤 1)**
- `grc-check-identity-provider`:`CommonRiskEventIdentityProcessor` / `RiskIdentityServiceImpl` / `RiskIdentityFacadeImpl` / `CheckRiskCisTicketValidProcessor`(CAPTCHA/OTP 风控),经 [[svc_cgs]] 暴露 `/api/cgs/risk-identify/*`。

**③ BMOC 审批(basis-merchant 编排 → merchant 建户 + 下游)**
- `basis-merchant` → `merchant`:`MerchantCreationClientImpl`(建户)、`PartnerClientImpl`(合作方)、`MerchantAddressClientImpl`(地址)、`MerchantMccClientImpl`(MCC)、`UfsOperationClientImpl`(文件)。
- `merchant` → 下游:**`AmlClientImpl` → [[svc_aml]]**(AML 风险,对应 AML Risk Calc)、`ProductAuditClientImpl` → [[svc_ppcenter]](产品审核/激活)、`StatementClientImpl` → [[svc_statementii]](对账单配置)、`MnsClientImpl`(通知/短信)。
- 审批通过发事件 → `payroll-core-service.CorporateListener`(WPS 企业同步)等订阅方消费(激活联动 [[svc_ppcenter]] / [[svc_statementii]] / [[svc_contract]] / [[svc_vis]])。

**④ 渠道报备(激活后,可收款前提)**
- `router` → `OnboardingClientImpl` / `RouteOnboardingProcessor`,`onboarding.OnboardingOrderAutoAdvanceJob` 自动推进报备单(见「渠道报备」节 + [[svc_cregister]])。

> Kibana 溯源方法与 mTID 陷阱见 skill `PayBy-service-callgraph`;UAT 后台会话较短,长表单期间可能超时,结果多已服务端持久化。

## 入驻库表影响范围(QA 校验)
跨库流程，按入驻链路顺序校验:Merchant → Member → Ppcenter → Dpm → Statementii → Contract → Vis。QA 库账号默认开通 SELECT/INSERT/UPDATE/DELETE，连接需指定库名(如 `merchantuser`)。

### Merchant 商户库(`merchant`)
| 表 | 用途 / 状态校验 |
| --- | --- |
| `t_merchant_creation_order` | 入驻申请单;审核通过后 Status=`ENABLED` |
| `t_merchant` | 商户主信息;审核通过后 Status=`MERCHANT_ENABLED` |
| `t_merchant_address` | 地址列表，类型 `["register","business"]` |
| `t_partner` | 合作伙伴信息 |
| `t_binding_card_apply_info` | 绑卡信息 |
| `t_merchant_biz_open` | 已开通业务 `["Acquire","WPS"]` |
| `t_biz_admin_info` | 业务管理员 `["SUPPER_ADMIN","ACQUIRE_ADMIN","WPS_ADMIN"]` |
| `t_merchant_acquire_info` | Acquire 业务信息 |
| `t_merchant_wps_info` | WPS 业务信息(开通 WPS 后) |
| `t_common_audit_order` | 公共审核单;WPS 审核 `audit_result=PASS` |
| `t_staff` / `t_staff_role` | 商户员工与角色 |

### Member 会员库(`member`)
| 表 | 用途 / 状态 |
| --- | --- |
| `tm_member` | 会员信息;0 未激活 → 1 激活 |
| `tm_member_identity` | 会员标识;0 未激活 → 1 激活 |
| `tr_member_account` | 基本账户 `BASIC`(Acquire)/ `WPS_SALARY`(WPS) |
| `tr_beneficiary_info` | 受益人卡信息 |

### 下游库
| 库.表 | 用途 |
| --- | --- |
| `ppcenter.t_product_apply_order` / `t_merchant_product_order` | 产品申请/已激活产品(Merchant VAM Topup) |
| `dpm.t_dpm_outer_account_subset` / `t_dpm_account_crl_def` | 外部账户分户 / 账户类型 |
| `statementii.t_settlement_config` | 对账单/结算配置 |
| `contract.t_contract` | 商户协议 |
| `vis.t_virtual_account` | 虚拟 IBAN 账户(Iban Top up);初始 Status=`Initial` |

## 商户注册来源
Unified Portal / Agent / Basis / Botim / 统一控台。BMOC `Merchant Approval` 列表 `Source` 字段常见 `AGENT`、`PORTAL`。

## 校验点
- 注册:OTP 登录后强制设密码;管理员手机号具备 administrator role。
- Acquire 激活:`t_merchant.Status=MERCHANT_ENABLED` 且 `tm_member` 状态=1。
- WPS 激活:`t_common_audit_order.audit_result=PASS`、`WPS_SALARY` 账户落地、`vis.t_virtual_account` 创建。
- 服务 Owner 对照、MPGS 组件依赖等开发侧信息(basis→onboarding→ppcenter/cmf→qpay-ni)见 [[svc_onboarding]] 与 [[reference_portal_env_access]];部分历史明细标「待补」。

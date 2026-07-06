---
id: scn_merchant_portal_registration
object_type: Scenario
name: Unified Portal 商户自助注册入驻向导(前端申请流程)
aliases: [merchant self onboarding, unified portal registration, 商户注册向导, corporate onboarding wizard, become a merchant]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-06'
source_type: uat_walkthrough
source_ref: 'UAT 实操:https://uat-web-unified.test2pay.com 全流程走查(Payment gateway / LLC / Mainland),2026-07'
tags: [merchant, onboarding, unified-portal, self-service, kyb, docusign, uat]
related_services: [svc_unified_merchant_portal, svc_merchant, svc_member, svc_basis_merchant, svc_contract]
related_tables: [tbl_merchant_t_merchant, tbl_merchant_t_merchant_creation_order]
related_scenarios: [scn_onboarding_manual_register]
---

# Unified Portal 商户自助注册入驻向导(前端申请流程)

> 商户在 **Botim Money Business** 统一门户(Unified Portal)自助提交入驻申请的**前端申请人视角**端到端走查(UAT 实操)。这是 [[flow_merchant_onboarding]] 的**申请提交阶段**的具体 UI 落地;提交后进入 BMOC 后台审核(AML + KYB)与激活的跨系统流程见 [[flow_merchant_onboarding]]。控台功能总览见 [[reference_merchant_portal_overview]],环境地址见 [[reference_portal_env_access]]。

## 触发 / 入口
- 地址(UAT):`https://uat-web-unified.test2pay.com/verify/login`(各环境见 [[reference_portal_env_access]])。
- **登录**:输入手机号(区号 +971)→ `Sign in/Sign Up` → OTP 校验。**UAT 登录需真实 OTP**;但**已在 BMOC 配置白名单的手机号 OTP 默认 `123456`**(测试用,如 `556579167`)。首次注册/新设备登录后**强制设置密码**,可能触发 2FA。管理员手机号即后续登录账号(administrator role)。
- 登录后进入 **Choose Merchant**(已有商户列表)→ 点 **`+ Add New Merchant`** 开始新入驻。

## 前置选择(4 连问,决定后续表单形态)
1. **What botim service do you need?** → `Payments`(收单)/ `Wage Protection System`(WPS 代发)。本走查选 **Payments**。
2. **Payments 子类型**(可多选)→ `Payment gateway`(网站直连收单)/ `Payment link` / `Point of Sales (POS)`。本走查选 **Payment gateway**。
3. **What type of business do you operate?** → `Sole Proprietor` / `Limited Liability Company (LLC)`。本走查选 **LLC**。
4. **What type of UAE business license do you have?** → `Freezone` / `Mainland`。本走查选 **Mainland**。

选完进入 **5 步向导**(顶部进度条):`Pricing → Company Profile → Business Information → Management → Review`,Review 之后是 **DocuSign 电子签约** → **Application Submitted**。每步右下角有 `Save Draft`(草稿),`Continue` 进入下一步。

## 步骤

### 1) Pricing(费率确认)
只读费率表 + 底部**必勾确认框**。
- **Card payments**:Domestic `2.4% + AED 1`、International `2.85% + AED 1`。
- **Additional pricing**:Card machine rental `-`、AliPay `1.90%`、Chargeback fee `AED 90`、AANI instant transfer `AED 3.50`、Bank transfer (VIBAN) `1.00%`、Setup fee `AED 1,500`、UnionPay (CUP) `2.50%`、Botim Pay `1.25%`、Refund fee `AED 1.50`。
- ✅ 勾选 "*I acknowledge that I have reviewed and agreed to the per-transaction fees, setup charges, and applicable service fees listed above, exclusive of 5% VAT.*" → `Continue`。

### 2) Company Profile(公司资料 + 证件)
- **Upload your trade license**(必传,JPG/PNG/PDF ≤5MB)。上传后系统尝试 OCR 自动带出公司资料。
- **License information**:Trade license authority(下拉:Abu Dhabi/Dubai/Sharjah/Ajman/Ras Al Khaimah/Umm Al Quwain/Fujairah/Free Zone)、License number、License issue date(日历,不可选未来日期)、License expiry date(选填)、Legal type(=LLC,随前置选择带出)。
- **Proof of address**:上传 **Tenancy Contract**(有效 Ejari 证书或等效租约,不接受水电账单)。
- **Registered address**:`Is the registered address the company address? Yes/No`、Country、Emirate、Area、Building number、Office number(选 Yes 时业务地址=注册地址)。
- **VAT certification details**:上传 **税务证书(Tax certificate)** + VAT registration number。
- **Bank account details**(账户与公司信息须一致):上传 **Bank statement or letter**、IBAN(后端校验)、Bank name、Account holder name、Address、Emirate、Country。
- 4 份必传文件:营业执照 / 租约 / 税务证书 / 银行流水。

### 3) Business Information(经营信息 + 3 个子问卷)
顶部字段:Company name、Website or social media link、Industry(下拉)、Monthly Turnover(下拉,如"expected payment volume p/m is AED 100,000 and above")、Payment Method Accepted(下拉,如 Card Payments)。
下方 **3 个必填折叠子节**(各自 `+ Add details` 打开独立子向导,完成后打绿勾):

- **① Tell us about your business**(3 步子向导:Business Overview → Business Size & Customers → Sales & Payment Details)
  - Business Overview:业务描述(≤240 字)、产品/服务 + 销售占比(需点 `+ Add new product` **提交成行**,否则报 "Please add at least one product")。
  - Business Size & Customers:员工数、UAE 分支数、客户类型(Individuals/Businesses)、主要结算币种(Dirham/US Dollar)、客户所在国家(搜索多选)。
  - Sales & Payment Details:预计月刷卡额/非卡额、平均/最高交易额、月交易笔数;card-present 占比(POS%/In-Store%)、月 POS 额、月 PayLink/QR/Gateway 额;Delivery timeline、Channel of Delivery(In-store/Delivery/Store pickup/Online·SaaS/Other)。
- **② Payment gateway API integration**(3 步子向导:Website & Customer Information → Privacy, Trust & Business Verification → Customer Verification & Card Security)
  - 一组 Yes/No 合规问答;选 **Yes** 会展开要求填**对应政策的网站 URL**(配送/退款/隐私政策、支付方式 logo 展示页)。
  - 含 TLS/SSL、域名所有权证明、年龄限制、是否存储持卡人数据(PAN/EXP/CVV — 使用网关的商户应选 **No**)、客户尽调(选 Yes 需描述尽调信息)、反欺诈措施、风控监控工具、拒付管理流程等**必填文本域**。
- **③ Compliance and sanctions**(单页 5 个 Yes/No)
  - 25%+ 股东/UBO 是否已披露(Yes)、是否无其他实体持 25%+(Yes)、近 10 年是否涉破产/债务重整(No)、是否有来自美国的收入(No)、是否有未决法律诉讼(No)。

### 4) Management(管理层 / 受益人)
- **Choose your document type**(如 Memorandum of agreement)+ **Upload your document**(抓取持股 >25% 的股东/合伙人)。
- **Assign company capacity**:系统尝试从文档识别代表;OCR 失败会提示 "*Failed to scan document. You can add members manually.*"。点 **`+ Add member`** 打开 **Management details** 弹窗:
  - Full name、Percentage(持股 %)、Role(多选:Signatory / Administrator / Shareholder)、Contact email、Contact mobile(+971)。
  - **Document information**:证件类型(Emirates ID / Passport)、Emirates ID 正/反面上传、Emirates ID number、Expiry date。
  - 保存后成员以绿勾卡片列出(可 Edit/删除)。

### 5) Review(汇总复核)
只读汇总:公司名 / 行业 / 网站 / 员工数、完整费率表、Company information、Business details(3 子节)、License information、Address+VAT+Bank details、Management details(附各文件名与所有字段)。
底部**必读确认声明**:"*We hereby acknowledge that all information provided in this summary … is accurate … By submitting these details, I confirm that I have read, understood, and agreed to the Privacy Policy and Terms and Conditions.*" → `Continue`。

### 6) DocuSign 电子签约(`/onboarding/onboarding-signing-doc`)
- 内嵌 **DocuSign**:勾选 "*I agree to use electronic records and signatures*"(Electronic Record and Signature Disclosure)→ DocuSign `Continue` → 采用/放置签名 → 完成 → 页面底部 `Submit`。
- ⚠️ 这是**具法律约束力的电子签署**,属申请人本人操作。

### 7) Application Submitted(`/onboarding/service-apply-successfully`)
- ✅ "**Application Submitted!** Your documents have been successfully received and are currently under review."
- **What happens next?**:Review Process(**2–3 个工作日**审核)· Email Confirmation(确认邮件发至登录账号邮箱)· Follow-up Contact(如需补料有代表联系)。
- 提供 **Download signed contract**(下载已签合同)。

## 校验点(QA)
- **草稿持久化**:会话超时(实测约几十分钟)会踢回登录页;重新登录 → `+ Add New Merchant` 会**保留已上传文件与部分选择**,但**并非全部字段**回填,需复核补齐。
- **前端字段校验**:license issue date 不可选未来;IBAN/邮箱/URL 格式校验;子问卷选 Yes 后其 URL/描述必填;产品行必须 `+ Add new product` 提交才计数。
- **提交后落库**(后端,详见 [[flow_merchant_onboarding]]):Merchant 库 `t_merchant_creation_order`(入驻申请单)、`t_merchant`(商户主信息,审核前非 ENABLED);Member 库 `tm_member`/`tm_member_identity` 处于未激活(状态 0)。
- **审核激活(两步)**:BMOC(LDAP 登录)`Basis Merchant => BUSINESS => Merchant => Merchant Onboarding`(注意不是 `Merchant Onboarding Management`=渠道报备)。待审行须 **先 `AML Risk Calc` 再 `KYB Approval`**:① AML 填 Risk Calculate 风险因子(Industry Type / Sanctions·PEP Screening / UBO Nationality / Business Profile / Product Services)→ `Save & Calculate` 得 Onboarding Risk Assessment+Score(实测 Medium/6.51),状态→`Awaiting KYB`;② KYB Approval 填 Result=PASS + Reason → `Confirm` → Status→`Approved`,商户激活(实测 Apply ID 2466)。表单字段与状态流转详见 [[flow_merchant_onboarding]] 步骤 3;通过后 `t_merchant.Status=MERCHANT_ENABLED`、`tm_member` 状态=1(见 [[reference_bmoc_basis_merchant]])。

## 关联
- 后端跨系统入驻流程(Acquire+WPS / BMOC 审核 / 库表影响):[[flow_merchant_onboarding]]。
- 控台功能与业务类型申请总览:[[reference_merchant_portal_overview]];环境地址与测试账号/OTP:[[reference_portal_env_access]]。
- 渠道报备(激活后可收款前提):[[svc_cregister]] / 人工报备 [[scn_onboarding_manual_register]]。
- 承载服务:[[svc_unified_merchant_portal]](门户前端)→ [[svc_merchant]] / [[svc_member]] / [[svc_basis_merchant]] / [[svc_contract]]。

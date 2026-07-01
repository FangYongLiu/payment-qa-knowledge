---
title: cgs-apitest payment 自动化测试模块总览
domain: acquire-transaction
kind: wiki_page
slug: cgs-apitest-payment-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: code_repo
source_ref: code_repo:caa31aee-5510-525f-9def-2ec2ccce0d9a
tags: []
related_services:
  - svc_3ds2
  - svc_acquireii
  - svc_cgs
  - svc_cgs_apitest
  - svc_cmf
  - svc_dpm_manager
  - svc_kyc
  - svc_member
  - svc_pbs
  - svc_pns
  - svc_protocol
  - svc_qpay_mpgs
  - svc_qpay_zand
  - svc_sgs
  - svc_tradeii
---

# cgs-apitest payment 自动化测试模块总览

cgs-apitest 的 `testcases/payment` 模块基于 pytest 驱动，围绕业务域 `acquire-transaction` 覆盖会员账户体系、KYC、绑卡/绑 IBAN、支付密码、扣款顺序、收银台与 MPGS 等渠道支付的端到端自动化测试。源代码位于 `cgs-apitest` 仓库 `testcases/payment`，共 52 个测试文件 + 25 个被引用的封装/工具源码。

## 测试覆盖的业务场景

按主题归类，每个主题进入对应专题页：

- **KYC 与用户准备**：EID Journey、NON-KYC 静默注册、KYC FINISH 用户复用、E2E 新用户 → KYC → ZAND IBAN 分配、白名单 ZAND IBAN 校验 → [[cgs-apitest-kyc-user-fixtures]]
- **会员 Profile 浏览**：EID-KYC（有效/过期）、NON-KYC、CDD0、Passport-KYC、VIP、VVIP 多 KYC 等级的 Profile 与限额 → [[cgs-apitest-member-profile-cases]]
- **绑/解卡与绑/解 IBAN**：NO-KYC / KYC / VIP 绑解支付卡、卡列表查询、KYC/VIP/VVIP 绑解 IBAN，含多张表数据校验 → [[cgs-apitest-bind-card-iban-cases]]
- **登录、注册与账户注销**：手机 OTP 注册、密码登录、OTP 登录、BOTIM 静默注册/登录、正常注销 / 数字货币注销 / 在途交易拒绝 → [[cgs-apitest-login-register-cases]]
- **账单 / Profile 资料 / 支付密码**：账单列表与详情、头像/昵称、付款码场景下对端资料、收银台首设/设置/修改/忘记（未登录、已登录、收银台）支付密码 → [[cgs-apitest-payment-password-cases]]
- **扣款顺序与账户余额**：付款码与全局代扣（AutoDebit）的扣款顺序设置、AED BASIC 账户余额与 DPM 子账户一致性 → [[cgs-apitest-deduct-order-balance-cases]]
- **MPGS 渠道支付**：DirectPay 3DS2（MPGS101–104）、MOTO 带/不带 CVV（MPGS105–112）、设备支付 MPGS131（ApplePay/GooglePay/SamsungPay）、卡组织拆分路由、全额/部分退款、AD 两阶段 Void → [[cgs-apitest-mpgs-channel-cases]]

详见自动化资产 [[auto_cgs_apitest_payment]]，以及关联场景 [[scn_mpgs_directpay_3ds2]]、[[scn_mpgs_moto_payment]]、[[scn_mpgs_device_pay]]、[[scn_mpgs_cardorg_split]]、[[scn_mpgs_refund_void]]。

## 通用文件结构与命名

- 测试根目录：`testcases/payment`，文件按主题命名，常见前缀：
  - `test_KYC_*` / `test_login_*` / `test_delete_account_*` / `test_member_*` / `test_password_*`
  - `test_mpgs*`、`test_*deduct*`、`test_query_balance` 等
- 测试数据通过 `get_testdata` fixture 按测试方法名作为 key 从 YAML 拉取参数化元组列表。
- 用例标记：`@pytest.mark.uat` / `@pytest.mark.sim` / `@pytest.mark.regression`；UAT 限定用例使用 `skip_if_not_uat`；个别 BUG 关联用例使用 `@pytest.mark.skip`。
- 注释 `notes("uat pass")` 用于标识在 UAT 环境已验证通过的用例。

## 核心 Fixtures

- `get_env`：当前环境名（sim / uat 等）。
- `get_urls`：返回 `cgs_url`、`sgs_url`。
- `get_env_data`：环境上下文配置。
- `db_instance_factory(role)`：按角色返回 DB 句柄，支持 `select_sql` / `execute_sql`，常用 role 包括 `select` / `member` / `dpm` / `protocol` / `tradeii` / `acquireii` / `cmf` / `pbsdb` / `pns`。
- `get_testdata`：按测试方法名解析 YAML 参数集。
- `get_redis_conf`：支付密码 / 风控相关用例的 Redis 缓存清理（前缀 `gp005_member`、`PayPwdValidate` 等）。
- `setup`（autouse）：实例化 `CGSapi`、`SGS`、`Module`、`RSA_encrypt`，部分主题额外注入 `MPGS3DS2Client(env)`、`ZandMigrationCGS`。

## 主要封装类

### `Module`（`API.payment_api.module`）

业务级组合操作，常用方法：
- `login(partner_id, uid, mobile_no) -> (access_key, pts_token)`
- `payby_login(mobile, password) -> (accessKey, ptsToken, mid, partnerId)`
- `create_non_kyc_user()` / `get_kyc_user()` / `create_zand_kyc_user()` / `get_zand_kyc_user()`
- `bind_card(...)` / `remove_bank_card(...)`（`kyc_status` 取 `NON_KYC` / `KYC_FINISH`，`is_first` 取 `'Y'/'N'`）
- `bind_iban(...)` / `remove_bank_account(...)`
- `deposit_submit(...)`、`cashdesk_pay(...)`、`cashdesk_pay_password(...)`

### `CGSapi`（`API.payment_api.cgs`）

直接封装 CGS 接口，主题覆盖：
- 注销：`personal_logout_init` / `queryReason` / `saveReason` / `check` / `queryBalance` / `identifyMethods` / `personal_member_logout`
- 登录与识别：`ups_identify_mobile`、`risk_unauth_sendIdentityOtp` / `verifyIdentityOtp`、`cashier_login_unauth_verify`、`cashier_unauth_initTrade` / `confirmPay` / `queryResult` / `queryTradeResult`
- 会员资料：`ups_publicfileUpload` / `ups_userProfileModify` / `ups_userProfileQuery` / `ups_transferOfMid`
- 账单：`personal_bill_list` / `personal_billDetail`
- 绑卡查询与扣款偏好：`personal_queryCardList`、`cashdesk_reloadDeductChannel(type)`、`personal_member_preference_save(value, type)`
- 余额：`personal_query_account_info(accountTypeList=["BASIC"])`
- 换号：`personal_mobile_changeInit` / `changeSendotp` / `personal_mobile_change`
- 风控：`risk_query_available_modes`、`risk_check_payment_password_v1`
- 收款码：`cashdesk_buildStaticCode`、`ptp_auth_parse`
- 3DS

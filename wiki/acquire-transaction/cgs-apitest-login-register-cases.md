---
title: 会员登录、注册与注销测试用例
domain: acquire-transaction
kind: wiki_page
slug: cgs-apitest-login-register-cases
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: code_repo
source_ref: code_repo:caa31aee-5510-525f-9def-2ec2ccce0d9a
tags: []
---

# 会员登录、注册与注销测试用例

覆盖 PayBy 会员核心生命周期接口：手机号 OTP 注册、密码登录、OTP 登录、BOTIM 静默注册/静默登录，以及账户注销（正常、数字货币用户、在途交易拒绝）三类场景的端到端用例与数据校验。

## 登录与注册用例

均位于 `test_login_xiaoyan.py`，统一支付密码 `132580`，标记 `@pytest.mark.sim`（部分附 `uat` 与 `notes("uat pass")`）。

| 用例 | 方法 | 场景 |
|---|---|---|
| N101 | `test_regist_by_opt` | 未注册手机号 OTP 注册 + 设置支付密码 |
| N102 | `test_login_by_password` | 注册用户 `USERNAME_PASSWORD_LOGIN` 模式密码登录 |
| N103 | `test_login_setPassword` | 注册用户 OTP 验证后重新设置支付密码 |
| N104 | `test_login_by_otp` | 注册手机号 OTP 登录（取 `identifyOptions[1]` 作为 OTP 凭证） |
| N105 | `test_regist_by_silent` | BOTIM 静默注册（AuthGuard → 协议签订 → push public key → ConfirmGuard） |
| N107 | `test_login_by_silent` | BOTIM 静默登录（SGS `auth_token` 换取 token 后 `personal_auth_login`） |

### 关键接口

身份识别与 OTP：
- `ups_identify_mobile(mobile)`：手机号识别，返回 `identifyOptions[]`，`[0]` 为密码项，`[1]` 为 OTP 项，每项含 `identifyTicket`
- `risk_unauth_sendIdentityOtp(identifyTicket)` → `otpTicket`
- `risk_unauth_verifyIdentityOtp(identifyTicket, otpTicket)`

BOTIM 静默注册/登录：
- partner 静默登录 → AuthGuard
- 协议查询/签订 `PAYBY_AUTH`
- push public key
- ConfirmGuard
- SGS `auth_token` 换取 token
- CGS `personal_auth_login` 完成 BOTIM-Pay 登录（详见 [[api_personal_v3_auth_login]]）

支付密码相关清理见 [[cgs-apitest-payment-password-cases]]。

### 数据准备与清理

- 注册类用例前后清理：`member.tm_member`、`member.tm_member_identity`、`member.tr_verify_ref` 等表（详见 [[tbl_member_db]]），以及 Redis `gp005_member`、`PayPwdValidate` 前缀缓存。
- 手机号通过 `utils.RSA.RSA_encrypt` 生成/加密。

## 账户注销用例

位于 `test_delete_account_xiaoyan.py`，覆盖正常、数字货币、在途交易三种分支。

| 用例 | 方法 | 标记 | 说明 |
|---|---|---|---|
| N101 | `test_deleteAccount` | skip | 普通用户正常注销端到端 + 重新注册回放 |
| N103 | `test_deleteAccountN103` | skip | 数字货币用户注销（`balanceStatus=Y`） + 重新注册回放 |
| E103 | `test_deleteAccountE103` | `sim`，active | 存在在途交易，提交注销被拒 |

### 注销流程编排

按以下顺序调用 CGS 接口：

1. `personal_logout_init(accessKey, ptsToken)` → 响应 body 含 `memberId`
2. `personal_logout_queryReason` → 可选注销原因列表
3. `personal_logout_saveReason(reasonId, reasonType)`
   - N101/N103 使用 `(1, 'TYPE1')`
   - E103 使用 `(11, 'TYPE11')`
4. `personal_logout_check` → 注销前置业务校验
5. `personal_logout_queryBalance` → 返回 `balanceStatus`
   - `Y`：可注销/可放弃
   - `N`：存在在途交易
6. `personal_logout_identifyMethods` → 返回 `identifyTicket`
7. `personal_member_logout(identifyTicket)` → 提交注销

### 关键状态与失败响应

- 正常/数字货币注销：`balanceStatus=Y`，提交后落库 `memberfront.t_apply.status=INIT` 等待人工审核，审核通过后核账户表（`tm_member.LOCK_STATUS` / `STATUS`）改为已注销态。
- 在途交易拒绝（E103）：`balanceStatus=N`，最终 `personal_member_logout` 返回：
  ```json
  {"code":"500","msg":"Remote call fail"}
  ```

### 注销后回放注册

N101/N103 注销完成后，使用同一手机号重新走 OTP 注册并设置支付密码，验证号码可被释放并重新可用。

## 共用 Fixtures 与数据

- `get_env` / `get_urls`（`cgs_url`、`sgs_url`） / `get_env_data`
- `get_testdata`：按方法名拆 key 提供参数化（`partner_id`、`uid`、`mobile_no`、`except_msg`、`kyc_msg` 等）
- `db_instance_factory`：注册/注销用例覆盖 `member`、`memberfront`、`protocol` 多库
- `get_redis_conf`：用于清理 `gp005_member`、`PayPwdValidate` 前缀缓存
- 工具：`utils.RSA.RSA_encrypt`、`utils.sendDubbo.call_dubbo_service`、`utils.pay_password_utils.clear_pay_password`、`utils.redis_utils`
- 业务封装：`Module.login(partner_id, uid, mobile_no) -> (access_key, pts_token)`、`Module.payby_login(mobile, password)`

## 涉及 DB 表

- `memberfront.t_member_logout_reason`：注销原因表
- `memberfront.t_apply`：注销申请审核表，`status=INIT`
- `member.tm_member`：核心账户表，`LOCK_STATUS` / `STATUS`
- `member.tm_member_identity`：手机号绑定关系
- `member.tr_verify_ref`：校验关系表

更多会员库表结构见 [[tbl_member_db]]；与之联动的 KYC 用户准备见 [[cgs-apitest-kyc-user-fixtures]]，绑卡/绑 IBAN 与注销前置依赖见 [[cgs-apitest-bind-card-iban-cases]]，模块总览参见 [[cgs-apitest-payment-overview]]。

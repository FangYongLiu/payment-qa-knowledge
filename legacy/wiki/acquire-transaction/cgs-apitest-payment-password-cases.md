---
title: 支付密码设置/修改/忘记测试用例
domain: acquire-transaction
kind: wiki_page
slug: cgs-apitest-payment-password-cases
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: code_repo
source_ref: code_repo:caa31aee-5510-525f-9def-2ec2ccce0d9a
tags: []
---

# 支付密码设置/修改/修改/忘记测试用例

覆盖会员支付密码在收银台首设、登录态设置/修改、未登录与已登录态忘记密码、以及收银台流程中触发忘记密码的完整端到端用例，并配套清理 DB 中的支付密码记录与 Redis 风控缓存。

## 用例编号 / 测试方法

文件：`test_password_xiaoyan.py::TestPassword`，全部标记 `@pytest.mark.sim`。

| 用例 | 方法 | 场景 |
|---|---|---|
| case1 | `test_set_password_cashier` | 未设支付密码用户通过转账触发收银台时完成首设 |
| case2 | `test_set_password` | botim 登录后直接设置支付密码 |
| case3 | `test_modify_password` | botim 登录后已设密用户走"修改初始化 → 风控验密 → 修改"，并在用例末还原原密码 |
| case4 | `test_forget_password_no_login` | 未登录态通过手机号识别 + 风控 OTP 重置支付密码 |
| case5 | `test_forget_password` | 已登录授权态忘记 + 重置支付密码 |
| case6 | `test_forget_password_cashier` | 收银台流程中触发授权态忘记密码并重置 |

## 前置条件 / Fixtures

- `setup`（autouse）注入：`get_env`、`get_urls`（取 `cgs_url`、`sgs_url`）、`get_env_data`、`db_instance_factory`、`get_testdata`、`get_redis_conf`。
- 实例化：`CGSapi(cgs_url, env_data, db_instance_factory)`、`Module(env_data, db_instance_factory)`、`RSA_encrypt(env_data, db_instance_factory)`。
- 测试数据按方法名取 yaml key：`test_set_password_cashier`、`test_set_password`、`test_modify_password`、`test_forget_password_no_login`、`test_forget_password`、`test_forget_password_cashier`。
- 统一支付密码值：`132580`。
- 相关用户准备见 [[cgs-apitest-kyc-user-fixtures]]。

## 数据清理（DB + Redis）

调用 `utils.pay_password_utils.clear_pay_password(db_instance_factory, redis_conf, uid)`：
- 清除 DB 表 `member.tr_password` 中该 uid 的支付密码记录。
- 清除 Redis `PayPwdValidate` 缓存（风控验密缓存）。
- 关联 `member.tm_operator` 用于读取/还原旧密码。

`test_modify_password` 末尾通过查询出的旧密码反向写回 DB，保证用例幂等。

## 被测接口 / 方法（含真实参数）

### 登录辅助（`Module`）
- `login(partner_id, uid, mobile_no) -> (access_key, pts_token)`：partner 站点登录。
- `payby_login(mobile, password) -> (accessKey, ptsToken, mid, partnerId)`：PayBy 手机号 + 密码登录。
- `cashdesk_pay_password(access_key, pts_token, token, channel='01', psw, except_msg) -> paymentOrderNo`：收银台密码支付（用于 case1/case6 收银台串联）。

### 设置 / 修改（`CGSapi`）
- 设置支付密码：登录态直接提交新密码 `132580`。
- 修改支付密码：
  1. 修改初始化，获取 `identifyTicket`。
  2. `risk_query_available_modes(identifyTicket, scene='...')` 查询可用验密方式。
  3. `risk_check_payment_password_v1(access_key, pts_token, pwd, identifyTicket)` 验证旧密码，响应含 `"result":"pass"`。
  4. 提交新支付密码。

### 未登录态忘记密码（case4）
- `ups_identify_mobile(mobile_no)`：手机号识别，返回 `body.identifyOptions[0].identifyTicket`（密码项）/`[1]`（OTP 项）。
- `risk_unauth_sendIdentityOtp(identifyTicket)` → `otpTicket`。
- `risk_unauth_verifyIdentityOtp(identifyTicket, otpTicket)`：OTP 校验通过后取重置令牌。
- 提交新支付密码完成重置。

### 已登录态忘记密码（case5）
- 授权态忘记密码初始化获取 `identifyTicket`。
- 发 OTP → 验 OTP → 提交新支付密码。

### 收银台首设 / 忘记（case1 / case6）
- 通过 `personal_mobile_init(access_key, pts_token, payeeMobile)` 等手机号转账接口下单进入收银台。
- 收银台未设密时进入首设流程；case6 在收银台内触发授权态忘记密码后重置。
- 重置后通过 `cashdesk_pay_password(...)` 用新密码完成支付，返回 `paymentOrderNo`。

## 关键校验点

- 首次设置：`member.tr_password` 中生成该 uid 的密码记录。
- 修改成功：风控 `risk_check_payment_password_v1` 返回 `"result":"pass"` 才能提交新密码。
- 忘记密码（未登录）：依赖 `ups_identify_mobile` 返回的 `identifyOptions` 数组定位 OTP 项后走风控 OTP。
- 忘记密码（收银台）：重置完成后用新密码在收银台支付应成功获得 `paymentOrderNo`。
- 用例末通过 `clear_pay_password` + DB 还原，保证下次运行可重入。

## 关联

- 登录 / OTP 注册中的支付密码首设入口见 [[cgs-apitest-login-register-cases]]。
- 测试模块总览见 [[cgs-apitest-payment-overview]]。
- 同一 `Module` / `CGSapi` 封装也用于 [[cgs-apitest-bind-card-iban-cases]] 与 [[cgs-apitest-deduct-order-balance-cases]]。

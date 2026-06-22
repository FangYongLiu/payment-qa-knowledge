---
title: 会员Profile与多KYC等级浏览用例
domain: acquire-transaction
kind: wiki_page
slug: cgs-apitest-member-profile-cases
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: code_repo
source_ref: code_repo:caa31aee-5510-525f-9def-2ec2ccce0d9a
tags: []
---

# 会员Profile与多KYC等级浏览用例

针对不同 KYC 等级（EID-KYC 有效/过期、NON-KYC、CDD0、Passport-KYC、VIP、VVIP）会员的 Profile 浏览与限额查询测试，验证 KYC 状态展示与会员等级显示的正确性。测试来源于 `testcases/payment/test_KYC_xinwei.py`。

## 覆盖的会员等级矩阵

| 测试方法 | 场景 | KYC 类型 | 备注 |
|---|---|---|---|
| `test_EID_KYC_profile` | EID-KYC 有效用户 Profile 浏览与限额 | EID | `kyc_level=2`，状态 VALID |
| `test_EID_KYC_profile_EID_EXPIRY` | EID 过期用户 Profile 浏览 | EID | EID 已过期 |
| `test_NOKYC_profile` | 未实名用户 Profile（未绑卡） | NON | 仅 silent registration |
| `test_CDD0_profile` | 绑卡未 KYC 的 CDD0 用户 | CDD0 | `kyc_level=0`，已绑支付卡 |
| `test_passport_KYC_profile` | 护照 KYC 用户 Profile | Passport | 护照路径 KYC FINISH |
| `test_VIP_KYC_profile` | VIP 会员 Profile | VIP | `memberLevel=VIP` |
| `test_VVIP_KYC_profile` | VVIP 会员 Profile | VVIP | `memberLevel=VVIP` |

## 前置条件 / Fixtures

- `setup`（autouse）注入：`get_env`、`get_urls`（`cgs_url`、`sgs_url`）、`get_env_data`、`db_instance_factory`、`get_testdata`。
- 实例化封装：`CGSapi`、`ZandMigrationCGS`、`Module`。
- 测试数据从 `get_testdata` 按测试方法名取参数化列表，字段包含 `partner_id`、`uid` / `mid`、`mobile_no`、`except_msg`、`kyc_msg`、`memberLevel` 等。
- 不同等级用户由 [[cgs-apitest-kyc-user-fixtures]] 提供的方式预置（mock SQL、白名单或自动化创建）。
- 测试标记：`@pytest.mark.regression` / `@pytest.mark.sim` / `@pytest.mark.uat`。

## 被测接口 / 方法

通过 `Module.login(partner_id, uid/mid, mobile_no)` 获取 `access_key`、`pts_token` 后，调用 CGS 端 Profile/KYC 查询接口完成 Profile 与限额校验。涉及到的核心接口：

- [[api_kyc_inquire_info]] — 查询 KYC 状态与 EID/Passport 信息。
- [[api_kyc_check_reminder]] — 取 KYC 状态提醒，判断是否过期/需要续期。
- 会员 Profile 与限额查询（通过 `CGSapi` 对应方法读取昵称、`kycStatus`、`memberLevel` 与限额）。
- 数据库侧校验 [[tbl_member_db]] 内 `kyc_level`、KYC 状态、会员等级字段。

## 各等级断言要点

- **EID-KYC（有效）**：`kycStatus` 为 KYC FINISH，`kyc_level=2`，KYC 状态 `VALID`，限额按 EID-KYC 等级展示。
- **EID-KYC（过期）**：EID 信息存在但已过期，`check-reminder` / `inquire-info` 应反映过期态，限额降级。
- **NON-KYC**：无 EID/Passport 信息，状态 `NON`，限额按未实名展示。
- **CDD0**：已通过快捷绑卡升级（`kyc_level=0`，绑卡场景 `QUICK_PAY`），但未完成正式 KYC；详见 [[cgs-apitest-bind-card-iban-cases]]。
- **Passport-KYC**：通过护照通道完成 KYC，`inquire-info` 返回 `passportInfo`。
- **VIP / VVIP**：`memberLevel` 分别为 VIP/VVIP，对应限额与 Profile 字段。

## 相关页面

- 用户复用与不同等级用户准备方式：[[cgs-apitest-kyc-user-fixtures]]
- 会员绑卡触发 CDD0 升级：[[cgs-apitest-bind-card-iban-cases]]
- 模块总览：[[cgs-apitest-payment-overview]]

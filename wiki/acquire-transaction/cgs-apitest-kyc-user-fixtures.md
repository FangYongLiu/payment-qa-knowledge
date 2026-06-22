---
title: KYC用户准备与复用测试方案
domain: acquire-transaction
kind: wiki_page
slug: cgs-apitest-kyc-user-fixtures
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: code_repo
source_ref: code_repo:caa31aee-5510-525f-9def-2ec2ccce0d9a
tags: []
---

# KYC用户准备与复用测试方案

本页归纳 `cgs-apitest` payment 自动化中与 KYC 用户构造、复用相关的测试用例集（`test_KYC_eid_journey_Nitin.py` 中的 TC8/TC9/TC10/TC11），覆盖 NON-KYC 用户即时创建、KYC FINISH 预置用户复用、E2E 新用户到 ZAND IBAN 分配，以及白名单 ZAND KYC 用户数据校验四类典型 fixtures 与场景。同模块下的 EID Journey 节点级用例（TC1–TC7）当前均为 skip，本页不展开。其他 KYC 等级 Profile 用例见 [[cgs-apitest-member-profile-cases]]，总体模块说明见 [[cgs-apitest-payment-overview]]。

## 用例编号与方法

| 用例 | 方法 | 说明 | 标记 |
|---|---|---|---|
| TC8 | `test_get_kyc_user` | 复用 mock 预置的 KYC FINISH 用户 | active |
| TC9 | `test_create_non_kyc_user` | 自动化静默注册创建 NON-KYC 用户 | active |
| TC10 | `test_e2e_new_user_to_zand_iban` | E2E 新用户 → KYC FINISH → ZAND IBAN 分配 + 钱包 ACTIVATED | active |
| TC11 | `test_zand_iban_assigned` | 白名单 KYC 用户的 ZAND IBAN 校验（API + DB） | active |
| TC1–TC7 | EID journey 节点用例 | check-reminder / inquire-info / start-journey / inquire-industry / full journey / leave journey | `@pytest.mark.skip` |

## 前置条件与 Fixtures

- `setup`（autouse）注入：`get_env`、`get_urls`（`cgs_url`、`sgs_url`）、`get_env_data`、`db_instance_factory`、`get_testdata`。
- 业务封装：`CGSapi`、`Module`、`ZandMigrationCGS`。
- 测试数据按方法名取参数化列表，含 `partner_id`、`uid`、`mobile_no`、`except_msg`、`kyc_msg`、`memberLevel` 等。
- 运行标记：`@pytest.mark.regression` / `@pytest.mark.sim` / `@pytest.mark.uat`。
- Mock 数据要求：
  - **TC8**：通过 `kyc.tm_kyc_apply` SQL submit 预置 KYC FINISH 用户，固定 `nationality=India`、`industry=Technology`。
  - **TC11**：用户必须在 `VISII_KYC_MID_WHITELIST` 白名单内（示例 `1TZHXRCM` / `100000091371`）。
  - **TC10**：依赖真实 Signzy 实体接入 + `vam_auth_active` bypass。

## NON-KYC 用户即时创建（TC9）

- 调用 `Module.create_non_kyc_user()` 走 silent registration，返回 `{access_key, pts_token, uid, ...}`。
- 验证点：返回的凭证可直接用于 [[api_kyc_eid_start_journey]]（start-journey）发起 EID KYC，证明账号已具备发起 KYC 的最小态。
- 适用：所有需要"干净 NON-KYC 账号"做隔离的下游用例（绑卡首绑、KYC 升级、收银台首付 OTP 等）。

## KYC FINISH 预置用户复用（TC8）

- 调用 `Module.get_kyc_user()` 取出预置 KYC FINISH 用户，返回 `{access_key, pts_token, member_id, ...}`。
- 校验：
  - 通过 [[api_kyc_inquire_info]]（inquire-info）查询，断言返回包含 `eidInfo`、`passportInfo`，nationality / industry 为 `India` / `Technology`。
  - DB 侧（[[tbl_member_db]] 内 KYC 相关表）核对 `kyc_level=2`、`status=VALID`。
- 适用：所有需要"已 KYC 用户"快速进入业务（绑 IBAN、ZAND 出款、限额提升场景等），无需每次跑完整 EID journey。

## E2E 新用户到 ZAND IBAN（TC10）

- 调用 `Module.create_zand_kyc_user()`，端到端串联：silent 注册 → 完整 EID KYC → ZAND 虚拟账户 IBAN 分配 → 钱包激活。
- 返回 `{access_key, pts_token, uid, iban, ...}`。
- 验证点：
  - `iban` 非空且按 AE/AED 规则分配。
  - 钱包状态最终为 `ACTIVATED`。
- 依赖：真实 Signzy KYC 通道 + `vam_auth_active` bypass 配置。
- 适用：需要"开户即出 IBAN"的 ZAND 出款/转账下游场景，可关联 [[scn_vam_iban_apply_and_transaction]]、[[scn_zand_fundout_test_cases]]。

## 白名单 ZAND KYC 用户校验（TC11）

- 调用 `Module.get_zand_kyc_user()` 取白名单内的现成 ZAND KYC 用户。
- 双向校验：
  - **API 侧**：账户/钱包接口返回 IBAN 已分配、钱包激活。
  - **DB 侧**：KYC 相关表（[[tbl_member_db]]）状态为 `kyc_level=2 / VALID`；ZAND IBAN 与会员账户绑定关系存在。
- 准入条件：`member_id` 必须命中 `VISII_KYC_MID_WHITELIST`（如 `1TZHXRCM` / `100000091371`），否则不会下发 ZAND IBAN。

## Module 封装方法速查

来自 `API.payment_api.module.Module`，本页四个 fixture 用例对应的核心 API：

- `login(partner_id, uid, mobile_no) -> (access_key, pts_token)`：常规登录拿凭证。
- `create_non_kyc_user() -> {access_key, pts_token, uid, ...}`：silent 注册全新 NON-KYC 用户。
- `get_kyc_user() -> {access_key, pts_token, member_id, ...}`：取预置 KYC FINISH 用户（India / Technology）。
- `create_zand_kyc_user() -> {access_key, pts_token, uid, iban, ...}`：E2E 创建用户 + KYC + ZAND IBAN（需 Signzy 实体 + `vam_auth_active` bypass）。
- `get_zand_kyc_user() -> {access_key, pts_token, member_id, ...}`：取白名单 ZAND KYC 用户。

## 选型建议

- 只要一个"可登录的空账号" → **TC9 / create_non_kyc_user**。
- 需要已通过 KYC、但不关心是否绑 IBAN → **TC8 / get_kyc_user**。
- 需要 KYC + ZAND IBAN 真实链路（出款、转账） → 优先 **TC11 / get_zand_kyc_user**（白名单，稳定），仅在必须验证"开户即开 IBAN"链

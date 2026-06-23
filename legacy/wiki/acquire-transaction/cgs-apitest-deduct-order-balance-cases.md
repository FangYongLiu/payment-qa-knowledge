---
title: 扣款顺序与账户余额测试用例
domain: acquire-transaction
kind: wiki_page
slug: cgs-apitest-deduct-order-balance-cases
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: code_repo
source_ref: code_repo:caa31aee-5510-525f-9def-2ec2ccce0d9a
tags: []
---

# 扣款顺序与账户余额测试用例

本页覆盖会员侧的**付款码/全局AutoDebit 默认扣款渠道设置**、**AED BASIC 账户余额查询及 DPM 一致性**校验，以及一个 **Dubbo 调用 KYC 查询的演示用例**。所有用例属于 `acquire-transaction` 业务域，数据由 `get_testdata` 按方法名注入。

## 用例清单

| 用例 | 方法 | 主题 |
|---|---|---|
| TC1 | `test_set_pay_deduct_balance` | 付款码扣款顺序 - 余额为首选 |
| TC2 | `test_set_pay_deduct_card` | 付款码扣款顺序 - 指定银行卡为首选 |
| TC3 | `test_set_pay_deduct_AutoDebit_balance` | 全局代扣扣款顺序 - 余额为首选 |
| TC4 | `test_set_pay_deduct_AutoDebit_card` | 全局代扣扣款顺序 - 指定银行卡为首选 |
| TC5 | `test_query_balance` | 查询 AED BASIC 账户余额并与 DPM 表对账 |
| N101 | `test_queryKycInfo` | Dubbo 调用 `IMemberKycFacade.queryKycInfo`（**skip**，仅 demo） |

## 扣款顺序设置（付款码 / 全局 AutoDebit）

TC1–TC4 验证会员在**付款码扫码**与**全局代扣（AutoDebit）**两类场景下，将"余额"或"指定银行卡"配置为默认扣款渠道的能力。

调用接口：
- `CGSapi.cashdesk_reloadDeductChannel(access_key, pts_token, type)`：拉取并刷新当前场景的可选扣款渠道列表，`type` 由 YAML 指定场景类别；响应需包含期望提示与 `defaultDeduct` 标识。
- `CGSapi.personal_member_preference_save(access_key, pts_token, value, type)`：保存偏好。
  - `value` = 偏好上下文（CONTEXT），余额或银行卡的标识。
  - `type` = 偏好类型（PREFERENCE_TYPE），与 YAML 字段对齐。

落库校验：
- `member.tr_member_preference (MEMBER_ID, CONTEXT, PREFERENCE_TYPE, status=1)`，按本次保存的 CONTEXT/PREFERENCE_TYPE 命中一条 `status=1` 记录。

前置：`Module.login(partner_id, uid, mobile)` 取 `access_key, pts_token`；银行卡相关用例需事先完成绑卡，参考 [[cgs-apitest-bind-card-iban-cases]]。

## AED BASIC 账户余额查询（TC5）

通过 `CGSapi.personal_query_account_info(access_key, pts_token, accountTypeList=["BASIC"])` 查询会员主账户余额：
- 响应路径：`body.accountList[0]`，字段 `accountStatus`、`balance`、`availableBalance`、`freezeBalance`。

一致性校验：
- API 返回的 `balance` 应等于 DPM 子账户表中**可用余额 + 冻结余额**之和。
- DPM 端数据来源见 [[tbl_dpm_db]]。

该用例同时作为余额类支付/出款（如 [[scn_mit_autodebit]]、[[scn_fundout_to_account]]）的基础数据接口验证。

## Dubbo KYC 查询 demo（N101，skip）

`test_queryKycInfo` 通过 `utils.sendDubbo.call_dubbo_service` 调用 `IMemberKycFacade.queryKycInfo`，作为 Dubbo 调用的样例保留，当前 `@pytest.mark.skip`，不参与回归。KYC 数据准备参见 [[cgs-apitest-kyc-user-fixtures]]，Profile 类用例见 [[cgs-apitest-member-profile-cases]]。

## 前置条件 / Fixtures

- `get_env` / `get_urls`（`cgs_url`、`sgs_url`）/ `get_env_data`：环境与基址。
- `db_instance_factory(role)`：按 `select`、`dpm`、`member` 等角色获取连接，覆盖以下库：
  - `member.tr_member_preference`（偏好落库）
  - `dpm.*` 子账户余额表（见 [[tbl_dpm_db]]）
- `get_testdata`：按方法名注入参数化数据。
- 实例化：`CGSapi`、`SGS`、`Module`。
- 标记：以 `@pytest.mark.sim` 为主，可在 UAT 环境运行。

## 关联

- 模块总览：[[cgs-apitest-payment-overview]] / [[auto_cgs_apitest_payment]]
- 偏好配置依赖的卡/IBAN 绑定：[[cgs-apitest-bind-card-iban-cases]]
- 余额查询接口在支付链路中的使用：[[api_payby_get_member_balance]]
- 代扣协议与渠道：[[tbl_deduct_t_deduct_protocol]]、[[tbl_member_tr_deduct_channel]]

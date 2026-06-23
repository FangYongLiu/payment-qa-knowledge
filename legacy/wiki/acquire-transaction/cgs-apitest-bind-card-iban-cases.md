---
title: 会员绑/解卡与绑/解IBAN测试用例
domain: acquire-transaction
kind: wiki_page
slug: cgs-apitest-bind-card-iban-cases
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: code_repo
source_ref: code_repo:caa31aee-5510-525f-9def-2ec2ccce0d9a
tags: []
---

# 会员绑/解卡与绑/解IBAN测试用例

覆盖 NO-KYC / KYC / VIP / VVIP 多等级会员在 PayBy 体系下，对支付卡（Quick Pay 快捷绑卡）与 IBAN 受益人账户的绑定 / 解绑流程，以及绑卡后的卡列表查询，配套核心表数据校验与前后清理。

## 用例编号 / 测试方法

| 用例 | 方法 | 说明 |
|---|---|---|
| N101 | `test_nokyc_bind_cards` | NO-KYC 会员绑→解支付卡全链路 + DB 校验 |
| N102 | `test_kyc_bind_cards` | 已 KYC 会员绑→解支付卡，断言 `EID/level=2` |
| N103 | `test_vip_bind_cards` | VIP 会员绑→解支付卡 |
| N104 | `test_query_cards_list` | 查询会员卡列表并核对 DB |
| N105 | `test_kyc_bind_iban` | KYC 会员绑→解 IBAN |
| N106 | `test_vip_bind_iban` | VIP KYC 会员绑→解 IBAN |
| N107 | `test_vvip_bind_iban` | VVIP 会员绑→解 IBAN |

标记：`@pytest.mark.uat` / `@pytest.mark.sim` / `@pytest.mark.notes("uat pass")`。

## 覆盖的业务场景

- **NO-KYC 会员绑/解支付卡**：未实名会员走 Quick Pay 快捷绑卡 → 解绑全流程，并校验银行卡表、代扣通道表、KYC 等级表、协议签约表四张表数据。
- **KYC 会员绑/解支付卡**：实名会员绑卡，KYC 等级以 `EID/level=2` 体现；解绑后协议为 `TERMINATED`，但 KYC 仍 `VALID`。
- **VIP 会员绑/解支付卡**：VIP 会员快捷绑卡，KYC 行状态为 `INVALID`（VIP 不通过该绑卡路径升级 KYC）。
- **绑卡用户查询卡列表**：[[api_payby_get_save_card]] `personal/queryCardList`，校验返回 `kycStatus=KYC_FINISH`、`bindCardScene=QUICK_PAY` 并定位对应 `tr_bank_account` 记录。
- **KYC / VIP / VVIP 会员绑/解 IBAN 账户**：通过 `bind_iban` / `remove_bank_account`，校验 IBAN 账户表状态在 `NORMAL ↔ DISABLED` 间切换。

## 前置条件 / Fixtures

- `setup`（autouse）注入：`get_env`、`get_urls`（取 `cgs_url`、`sgs_url`）、`get_env_data`、`db_instance_factory`、`get_testdata`。
- 实例化：`Module`（业务级组合操作）、`CGSapi`（CGS 接口）、`SGS`（SGS 接口）、`RSA_encrypt`（随机 token/code）。
- 测试数据由 `get_testdata` 以方法名为 key 提供参数化元组：partner_id、uid/mid、mobile_no、is_app、cardNo、iban、expireDate、cvv、holderName、bank_code、bank_name、city/city_code、except_msg 等。
- KYC 用户复用方案见 [[cgs-apitest-kyc-user-fixtures]]；会员登录与令牌获取见 [[cgs-apitest-login-register-cases]]。

## 被测接口 / 方法

### Module（业务封装 `API.payment_api.module`）
- `login(partner_id, uid/mid, mobile_no) -> (access_key, pts_token)`：会员登录。
- `bind_card(access_key, pts_token, except_msg, is_first, cardNo, expireDate, cvv, holderName, kyc_status, env=...) -> cardId`
  - `is_first='Y'`：首绑（NO-KYC 路径）；`'N'`：已 KYC 路径。
  - `kyc_status` 取 `NON_KYC` 或 `KYC_FINISH`。
- `remove_bank_card(access_key, pts_token, except_msg, cardId, kyc_status, is_app)`：解绑支付卡（对应 [[api_payby_remove_save_card]]）。
- `bind_iban(access_key, pts_token, except_msg, is_first, iban, bank_code, bank_name, city, holder_name='') -> accountId`：绑 IBAN 受益账户。
- `remove_bank_account(access_key, pts_token, except_msg, accountId, is_app)`：解绑 IBAN 账户。

### CGSapi
- `personal_queryCardList(access_key, pts_token, scene='payment')`：查询绑卡列表，响应 `cardList[*]` 含 `cardId`、`kycStatus`、`bindCardScene`。

## DB 校验点

绑/解卡涉及表（[[tbl_member_db]]、[[tbl_protocol_t_contract_sign_info]]）：

- `tr_bank_account`：绑卡记录主表，按 `cardId` / 会员 ID 定位。
- [[tbl_member_tr_deduct_channel]] `tr_deduct_channel`：代扣通道行，绑卡同步落入。
- 会员 KYC 等级行：
  - NO-KYC 首绑后建立 CDD0 等级（`kyc_level=0`）。
  - KYC 绑卡场景断言 `EID` 类型且 `level=2`。
  - VIP 路径下 KYC 行 `status=INVALID`，不通过快捷绑卡升级。
- [[tbl_protocol_t_contract_sign_info]]：绑卡产生签约协议；解绑后置 `TERMINATED`，但 KYC 行仍保持 `VALID`。
- IBAN 绑定校验 `tr_beneficiary_info`：
  - `country_code=AE`、`currency=AED`、`card_category=IBAN`
  - 状态切换 `NORMAL`（绑定后） ↔ `DISABLED`（解绑后）

## 数据清理（幂等保证）

测试前后通过 SQL 清理以下表，避免脏数据影响重跑：

- `tr_bank_account`
- `tr_deduct_channel`
- `protocol.t_contract_sign_info`
- `tr_beneficiary_info`

## 关联

- 总览：[[cgs-apitest-payment-overview]]
- 多 KYC 等级 Profile 浏览（含 CDD0 绑卡未 KYC 用户）：[[cgs-apitest-member-profile-cases]]
- 绑卡后续：扣款顺序设置与余额查询见 [[cgs-apitest-deduct-order-balance-cases]]；MPGS 渠道支付场景见 [[cgs-apitest-mpgs-channel-cases]]。

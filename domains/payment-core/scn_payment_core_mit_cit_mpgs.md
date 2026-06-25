---
id: scn_payment_core_mit_cit_mpgs
object_type: Scenario
name: MIT/CIT MPGS 循环（tokenized）支付测试
aliases:
- recurring payment
- 循环支付
- tokenized payment
- MIT/CIT
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/2095087700 + wiki:8d7a8617-1740-4670-8898-b035d5fdf23c
tags:
- MIT
- CIT
- MPGS
- recurring
- 3DS
- AutoDebit
- DirectPay
- PayAndSign
related_services:
- svc_sgs
- svc_payment
- svc_protocol
- svc_deduct
- svc_member
related_tables: [tbl_deduct_t_deduct_protocol, tbl_member_tr_bank_account, tbl_member_tr_bank_card_token]
- tbl_member_tr_bank_card_token
- tbl_acquireii_t_card_info
related_logs: []
---

# MIT/CIT MPGS 循环（tokenized）支付测试

## 背景

为提升整体支付成功率，业务侧需向外部大商户提供 tokenized（recurring）支付能力。CKO 通道的 tokenized payment 目前仅支持 Botim 业务，因此引入 **MPGS 通道**为其他外部商户开放循环支付。关联需求：MER-413 Recurring Payments (CIT/MIT)、MIT/CIT Second Phase、MIT/CIT Via MPGS；关联 Jira：PAYM-2235、PAYM-1558。

Tokenized 支付的优势：
- 后续交易（MIT）无需再触发 3DS 认证，成功率更高。
- 相比 MOTO 支付，chargeback 争议胜诉率更高。

术语：**CIT**=Customer Initiated Transaction（用户发起，首笔需 3DS + 签约）；**MIT**=Merchant Initiated Transaction（商户发起，基于已签协议自动扣款，无需 3DS）。

## 触发 / 入口

按四类 paySceneCode 经 [[api_payby_payment_create_order]] / SGS `/acquire2/placeOrder` 发起：

- **PayAndSign CIT**：SGS `/acquire2/placeOrder`，`paySceneCode=PAYANDSIGN`，`paySceneParams.protocolSceneCode=111`、`oneTimePayment=""`。进 paypage 用 payby/botim app 完成支付。
- **DirectPay 首次 CIT**：Create Order，`paySceneCode=DIRECTPAY`，携卡信息（FPN/DPN：`cardNo`/`holderName`/`cvv`/`expYear`/`expMonth`）+ `customerId` + 签约参数（`saveCard=true`、`agreementVersion=V1`、`agreementSign=True`、`protocolNotifyUrl`）+ `threeDSecure=true`、`source=INTERNET` + `agreementInfo`。
- **DirectPay 后续 CIT**：Create Order，`paySceneCode=DIRECTPAY`，用 `cardToken`（替代卡信息）+ `cvv` + `agreementInfo` + `source=INTERNET`。
- **AutoDebit MIT**：Create Order，`paySceneCode=AUTODEBIT`，用 `authProtocolNo`（即 deduct_protocol_no）+ `source=MERCHANT` + `agreementVersion=V1`，无需 3DS。

## 关联关系

- **涉及服务**：[[svc_sgs]]、[[svc_payment]]、[[svc_protocol]]、[[svc_deduct]]、[[svc_member]]（= `related_services`）
- **校验的表**：[[tbl_deduct_t_deduct_protocol]]、[[tbl_member_tr_bank_card_token]]、[[tbl_acquireii_t_card_info]]（= `related_tables`）
- **相关场景**：单笔直连/代扣基础场景见 [[scn_online_business_direct_pay]] 与 [[scn_online_business_auto_debit]]；3DS 降级导致代扣失败的排障见 [[ts_directpay_3ds_downgrade_token_invalid]]
- **签约协议接口**：[[api_payby_apply_protocol]] / [[api_payby_get_protocol]] / [[api_payby_protocol_notify]]（由 [[svc_protocol]] 暴露）

## 前置条件

ACS 配置（按 `MerchantId` 配置，用于命中 MPGS 通道路由）：
- `MerchantId`：测试 mid
- `paramKey = DEDUCT_INTERNAL_PARTNER`
- `paramValue = Y`

商户开通产品：
- Auto Debit
- Direct Pay Domestic Card
- Direct Pay INTL Card

CIT 路由要求：触发 3DS 验证，并路由至 MPGS（PAYANDSIGN 场景下路由至 cko/mpgs）通道。后续 CIT 需先拿到可用 `cardToken`（见下方 DB 校验点的取值 SQL）。

## 操作步骤

1. **PayAndSign CIT**：`/acquire2/placeOrder` 创建 PAYANDSIGN 订单 → 进 paypage 用 payby/botim app 完成卡支付（触发 3DS，路由 cko/mpgs）→ 成功后获取 `deduct_protocol_no`。
2. **DirectPay 首次 CIT**：Create Order（DIRECTPAY，带卡信息 + agreementInfo + customerId）→ 触发 3DS，路由 mpgs → 成功后获取 `deduct_protocol_no` 与 card token。
   示例 `agreementInfo`：`agreementType=RECURRING`、`numberOfPayments=1`、`amountVariability=VARIABLE`、`expiryDate=2035-01-01`、`paymentFrequency=DAILY`、`minimumDaysBetweenPayments=1`。
3. **DirectPay 后续 CIT**：Create Order（DIRECTPAY，用 `cardToken` + `cvv` + agreementInfo，`source=INTERNET`）。
4. **AutoDebit MIT**：Create Order（AUTODEBIT，用上面取得的 `authProtocolNo`，`source=MERCHANT`）发起商户侧自动扣款，无需 3DS。

## DB 校验点

- **协议表** [[tbl_deduct_t_deduct_protocol]]：
  ```sql
  select * from deduct.t_deduct_protocol
   where partner_id=200000054800 and status="A" order by create_time desc;
  ```
  - CIT 成功后新增一条数据，`status='Y'`，可取出 `deduct_protocol_no` 用于后续 MIT。
  - CKO 通道多次 CIT 成功：旧协议数据 `status` 被置为 `F`。
  - MPGS 通道多次 CIT 成功：持续生成新数据。
- **卡 token 表** [[tbl_member_tr_bank_card_token]]：
  ```sql
  select * from member.tr_bank_card_token
   where institution_code='MPGS' and status='Y' order by create_time desc;
  ```
  存在 `institution_code='MPGS'` 且 `status='Y'` 的记录表示 MPGS token 已建立。
- **取 cardToken**（后续 CIT 用）[[tbl_acquireii_t_card_info]] / `member.tr_bank_account`：
  ```sql
  select card_token from acquireii.t_card_info where global_id={global_id};
  select OUT_ACCOUNT_TOKEN from member.tr_bank_account
   where MEMBER_ID={mid} and STATUS=1 order by create_time desc;
  ```

## 预期结果

- CIT 成功后 `t_deduct_protocol` 生成 `status='Y'` 协议数据，`tr_bank_card_token` 中存在 `institution_code='MPGS'`、`status='Y'` 记录。
- 拿到 `deduct_protocol_no`（authProtocolNo）后可发起 AutoDebit MIT，后续交易经 MPGS 完成，无需再次 3DS。
- 日志中向 MPGS 发送的请求（`BankClientImpl`，URL 形如 `https://mtf.gateway.mastercard.com/api/rest/version/100/merchant/TEST461000000011/order/.../transaction/...`）应包含：
  - `agreement`：`type=RECURRING`、`id`、`expiryDate`、`numberOfPayments`、`amountVariability`、`minimumDaysBetweenPayments`、`paymentFrequency`
  - `apiOperation=PAY`、`sourceOfFunds.provided.card.storedOnFile=TO_BE_STORED`
  - `transaction.source=INTERNET`、`authentication.transactionId`

> 服务链中 authpay/cmf 等节点的精确穿越顺序在本对象未逐跳列出，以 cgs-apitest 回归与 callgraph 为准（部分标「待补」）。

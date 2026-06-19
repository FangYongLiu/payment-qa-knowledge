---
title: CKO订阅支付测试方法指南
domain: channel-integration
kind: wiki_page
slug: cko-subscription-test-guide
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2228977707
tags: []
---

# CKO订阅支付测试方法指南

本页给出 CKO 订阅支付在 QA 环境下的测试入口、收单场景构造、交易查询、配置约束以及数据校验维度。业务背景与路由原理见 [[cko-subscription-payment-overview]] 与 [[cko-subscription-routing-mechanism]]；收银台流程见 [[cko-subscription-cashier-flow]]。

## 测试卡号

- 有效期与 CVV 均不校验。
- 详细用例见 [[scn_cko_subscription_test_cards]]。

| 卡号 | 类型 |
|---|---|
| 4010 0617 0000 0021 | 本地卡 Debit |
| 5385 3083 6013 5181 | 本地卡 Credit |
| 4659 1055 6905 1157 | 外卡 Debit |
| 4242 4242 4242 4242 | 外卡 Credit |
| 4870 5270 1770 0692 | 认证拒绝 |
| 4544 2491 6767 3670 | 渠道返回失败（异常用） |

## 收单测试网关

- 网关：`http://qa.test2pay.com/manualTest/gateway/sgs`
- service：`acquire2/placeOrder`
- 测试商户 merchant：`200000036054`
- 业务参数通过 `bizContent` 传入，按 `paySceneCode` 区分场景。

## paySceneCode 场景

| paySceneCode | 场景 | 操作 / 关键参数 |
|---|---|---|
| `DYNQR` | 普通收单 | 取 `interActionParams` 中的 `tokenUrl` 生成二维码，App 扫码进入收银台 |
| `PAYANDSIGN` | 支付并签代扣 | `protocolSceneCode=111`；落库 [[tbl_deduct_t_deduct_protocol]]，`deduct_protocol_no` 可用于代扣 |
| `AUTODEBIT` | 代扣 | `authProtocolNo` = 协议号；提交后直接完成，无用户交互 |
| `PAYPAGE` | 匿名支付 | 携带 `redirectUrl` / `customerId` / `oneTimePayment`；浏览器直接打开 `tokenUrl`。**不支持订阅支付** |

### 协议号来源

- `PAYANDSIGN` 完成后：[[tbl_deduct_t_deduct_protocol]] `deduct_protocol_no`
- [[tbl_protocol_t_contract_sign_info]] `sign_contract_no`
- 二维码生成器：`https://cli.im/text`

## 交易查询

- 入口：`http://sim.intra.test2pay.com/basis/login`（域账户登录）
- 路径：综合管理 → 联合查询
- 订单号类型选 `product_order_no`，填收单返回的 `orderNo`

## 支付鉴权配置说明

- 配置表：[[tbl_cashdesk_t_filter_node]]
- 为保证测试环境与生产一致，支付鉴权配置由专属人员根据实际投产情况统一配置，**测试人员不可随意更改**。
- 商户 `200000036054` 一般已满足收单要求；鉴权不满足时联系配置负责人协助调整。

## 核身规则配置

在 basis → 风控管理 → 风控事件 → 核身规则管理 中操作：

1. 添加规则：
   - 事件类型：`payment`
   - 规则维度：`memberId`，运算符 `=`，数值填本人 mid
   - 核身方式：勾选目标项（`threeds`=3DS）
   - 优先级：`0`
2. 提交后在草稿状态找到该条，改为生效。
3. basis → 综合管理 → basis 审核 → 审核记录，审核通过后刷缓存生效。

## 数据校验维度

测试完成后从以下维度核对结果：

- **订单**：订单状态 + 实际路由渠道（`CKO101` / `CKO102` / `CKO111` / `CKO121`）
- **银行卡 / 协议**：
  - `tr_bank_account`
  - [[tbl_member_tr_bank_card_token]]：是否新增、`channel`、协议号、状态
  - [[tbl_member_tr_deduct_channel]]
- **日志**：各接口 `preferSign` / `frictionless` / `is3DS` 传参；CMF 返回 `signTransactionId` / `signSource`
- **风控**：DataEden 校验点（如 `CP-GR-000005`）、风控画像 `threeDSFlag`

## 路由结果速查矩阵

以"支付绑卡 / 已绑卡"场景为例，用于核对路由判定是否符合预期：

| preferSign | 核身 | 签约状态 | 签约渠道 | 路由结果 |
|---|---|---|---|---|
| Y | 3DS | 新卡 / 未签 | 可用 | CKO102 签约 |
| Y | 3DS | 新卡 / 未签 | 不可用 | CKO101 |
| Y | 密码 / 免密 | 未签约 | 可用 | 非 CKO102 |
| Y | 3DS | 已签约 | 可用 | CKO101（卡支付） |
| Y | 3DS | 已签约 | 不可用 | CKO102 重签 |
| Y | 密码 / 免密 | 已签约 | 可用 | CKO111 订阅 |
| Y | 密码 / 免密 | 已签约 | 不可用 | 非 CKO111 |
| N / Null | 3DS | 任意 | 可用 | CKO101 |
| N / Null | 密码 | 已签约 | 可用 | 非 CKO111 |

口径：`preferSign=Y` 且 `is3DS=Y` 才触发签约；已签约卡走密码 / 免密才命中 CKO111；`preferSign=N` 或 `Null` 一律不签约、不走订阅渠道。

完整时序见 [[flow_cko_subscription_payment]]。

---
title: CKO订阅支付测试指南
domain: channel-integration
kind: wiki_page
slug: cko-subscription-test-guide
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:5b35d40b-b532-44de-b69e-abffc289be85
tags: []
---

# CKO订阅支付测试指南

本页汇总 CKO 订阅支付在测试环境的执行方法，包括测试卡号、收单网关参数、paySceneCode 场景、交易查询入口、支付鉴权与核身规则配置，以及数据校验维度。完整业务背景见 [[cko-subscription-payment-overview]]，渠道角色见 [[cko-channel-definitions]]，系统流程见 [[cko-subscription-system-flow]]，端到端用例见 [[scn_cko_subscription_payment_cases]]。

## 测试卡号

有效期与 CVV 均不校验。

| 卡号 | 类型 |
|---|---|
| 4010 0617 0000 0021 | 本地卡 Debit |
| 5385 3083 6013 5181 | 本地卡 Credit |
| 4659 1055 6905 1157 | 外卡 Debit |
| 4242 4242 4242 4242 | 外卡 Credit |
| 4870 5270 1770 0692 | 认证拒绝 |
| 4544 2491 6767 3670 | 渠道返回失败（异常用） |

## 收单测试网关参数

- 网关：`http://qa.test2pay.com/manualTest/gateway/sgs`
- service：`acquire2/placeOrder`
- 测试商户 merchant：`200000036054`
- 业务参数通过 `bizContent` 传入，按 `paySceneCode` 区分场景
- 二维码生成器：`https://cli.im/text`

## paySceneCode 场景

| paySceneCode | 场景 | 操作 / 关键参数 |
|---|---|---|
| DYNQR | 普通收单 | 从 `interActionParams` 中取 `tokenUrl` 生成二维码，App 扫码进入收银台 |
| PAYANDSIGN | 支付并签代扣 | `protocolSceneCode=111`；落库 `t_deduct_protocol`，其 `deduct_protocol_no` 可用于代扣 |
| AUTODEBIT | 代扣 | `authProtocolNo` = 协议号；提交后直接完成，无需用户交互 |
| PAYPAGE | 匿名支付 | 携带 `redirectUrl` / `customerId` / `oneTimePayment`；浏览器直接打开 `tokenUrl` |

### 协议号来源

- PAYANDSIGN 成功后取 `t_deduct_protocol.deduct_protocol_no`
- 或取 `t_contract_sign_info.sign_contract_no`

## 交易查询

- 入口：`http://sim.intra.test2pay.com/basis/login`（域账户登录）
- 路径：综合管理 → 联合查询
- 订单号类型选 `product_order_no`，填入收单返回的 `orderNo`

## 支付鉴权配置说明

- 为保证测试与生产一致，支付鉴权配置由专属人员统一维护，测试人员不可随意更改。
- 商户 `200000036054` 一般已满足收单要求。
- 鉴权不满足时，联系配置负责人协助调整。
- 配置表：`t_filter_node`（cashdesk 库）；`unit_id=13` 已绑卡，`unit_id=4` 新绑卡。

## 核身规则配置

路径：basis → 风控管理 → 风控事件 → 核身规则管理。

添加规则：

- 事件类型：`payment`
- 规则维度：`memberId`，运算符 `=`，数值 = 本人 mid
- 核身方式：勾选目标项（`threeds` = 3DS）
- 优先级：`0`

提交后流程：

1. 在草稿状态下找到该条，改为生效
2. 进入 basis → 综合管理 → basis 审核 → 审核记录
3. 审核通过后刷缓存生效

## 数据校验维度

- **订单**：订单状态 + 实际路由渠道（CKO101 / 102 / 111 / 121）
- **银行卡 / 协议**：`tr_bank_account`、`tr_bank_card_token`（是否新增、`channel`、协议号、`status`）、`tr_deduct_channel`
- **日志**：各接口的 `preferSign` / `frictionless` / `is3DS` 传参，CMF 返回的 `signTransactionId` / `signSource`
- **风控**：DataEden 校验点（如 `CP-GR-000005`）、风控画像 `threeDSFlag`

## 路由结果速查矩阵

以「支付绑卡 / 已绑卡」场景为例：

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

要点：

- 仅当 `preferSign=Y` 且 `is3DS=Y` 才触发签约
- 已签约卡走密码 / 免密时命中 CKO111
- `preferSign=N / Null` 一律不签约、不走订阅渠道

## 测试用例覆盖

| 模块 | 用例数* | 覆盖要点 |
|---|---|---|
| 老收银台 | ~33+ | 充值 / 收单：新卡、已绑未签、已签；支付与签约；preferSign × 核身；异常流；鉴权 + 风控矩阵 |
| 新收银台 | ~16 | 标准收银台收单，同维度；异常流（处理中、失败、风控拒绝、补偿、绑卡上限） |
| 独立绑卡 | 7 | 是否签约（CKO121）、解绑、重绑、渠道处理中 / 失败 |
| 特殊业务 | ~24 | 付款码、PAYPAGE、代扣、facepay、authSign、国际汇款、灰度发布 |
| 回归 | 11 | PAYPAGE、BotIM 扫码、代扣、Direct Pay、收单、退款、超长扩展字段 |

\* 用例数为按用例编号统计的近似值。

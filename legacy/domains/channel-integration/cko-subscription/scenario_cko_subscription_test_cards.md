---
id: scn_cko_subscription_test_cards
object_type: Scenario
domain: channel-integration
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: confluence:AQ/2228977707
tags:
- cko
- subscription
- test-cards
- test-cases
subdomain: cko-subscription
module: testing
sensitivity: normal
name: CKO订阅支付测试卡用例
aliases: []
related_services: []
related_tables:
- tbl_member_tr_bank_card_token
- tbl_member_tr_deduct_channel
- tbl_deduct_t_deduct_protocol
- tbl_protocol_t_contract_sign_info
- tbl_cashdesk_t_filter_node
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
在 CKO 渠道订阅支付（[[cko-subscription-payment-overview]]）相关流程中，需要使用测试卡号进行：
- 绑卡（独立绑卡 / 支付绑卡）
- 收银台卡支付（老收银台 PayBy App / 新收银台 BotIM）
- 鉴权拒绝、渠道返回失败等异常场景验证
- 五大模块测试用例覆盖（老收银台 / 新收银台 / 独立绑卡 / 特殊业务 / 回归）

参考 Checkout 官网测试卡：https://www.checkout.com/docs/developer-resources/testing/test-cards

## 前置条件
- 业务方已配置「支持订阅支付」的支付鉴权（`t_filter_node`，由专属人员统一维护，测试人员不可随意更改；商户 `200000036054` 一般已满足收单要求）
- 已接入 CKO 渠道：CKO101（支付）/ CKO102（签约）/ CKO111（订阅/代扣）/ CKO121（独立绑卡）
- 核身规则已在 basis → 风控管理 → 风控事件 → 核身规则管理中配置并审核生效
- 测试卡有效期与 CVV 均不校验

## 操作步骤
### 一、扩充测试卡清单
| 卡号 Card | 类型 Type |
|---|---|
| 4010 0617 0000 0021 | 本地卡 Local · Debit |
| 5385 3083 6013 5181 | 本地卡 Local · Credit |
| 4659 1055 6905 1157 | 外卡 Foreign · Debit |
| 4242 4242 4242 4242 | 外卡 Foreign · Credit |
| 4870 5270 1770 0692 | 认证拒绝 Authentication rejected |
| 4544 2491 6767 3670 | 渠道返回失败 Channel failure（异常用） |

### 二、五大模块测试用例覆盖
| 模块 Module | 用例数* | 覆盖要点 |
|---|---|---|
| 老收银台 Old cashier (PayBy App) | ~33+ | 充值 / 收单：新卡、已绑未签、已签约的支付与签约；preferSign × 核身组合；异常流程；鉴权 + 风控矩阵 |
| 新收银台 New cashier (BotIM/cashierii) | ~16 | 标准收银台收单，同维度；异常流程（处理中、失败、风控拒绝、补偿、绑卡上限） |
| 独立绑卡 Standalone bind | 7 | 含/不含签约绑卡（CKO121）、解绑、重绑、渠道处理中/失败 |
| 特殊业务 Special | ~24 | 付款码、PAYPAGE、代扣支付、facepay、authSign、国际汇款、灰度发布 |
| 回归 Regression | 11 | PAYPAGE、BotIM 扫码、代扣、Direct Pay、收单、退款、扩展字段超长 |

*用例数为按用例编号统计的近似值。

### 三、收单测试入口
- 网关：`http://qa.test2pay.com/manualTest/gateway/sgs`
- service：`acquire2/placeOrder`
- 测试商户：`200000036054`
- 通过 `bizContent` 按 `paySceneCode` 区分场景：DYNQR / PAYANDSIGN / AUTODEBIT / PAYPAGE

## DB 校验点
- `member.tr_bank_card_token`：独立绑卡（CKO121）或支付绑卡签约成功后，校验是否落库；CKO 返回的 `signTransactionId` 加密后作为 `token` 落地；`channel` 应为签约渠道；`status=Y` 表示有效。该表是否存在有效数据作为该卡是否已签约的判断依据。
- `member.tr_bank_account`：`status` 1 已激活 / 0 已解绑 / 3 处理中；鉴权状态 1/0。
- `member.tr_deduct_channel`：独立绑卡含签约成功后新增。
- `deduct.t_deduct_protocol`：PAYANDSIGN 后落库，`deduct_protocol_no` 可用于代扣（AUTODEBIT 的 `authProtocolNo`）。
- `protocol.t_contract_sign_info`：`sign_contract_no` 即协议号。
- `cmf.tt_inst_order` / `tt_inst_result`：扩展字段记录渠道返回值。
- 订单查询入口：`http://sim.intra.test2pay.com/basis/login` → 综合管理 → 联合查询，订单号类型选 `product_order_no`。

## 预期结果
### 测试卡场景
- 本地卡 / 外卡（Debit / Credit）：可正常完成绑卡及收银台卡支付流程
- `4870 5270 1770 0692`：鉴权被拒绝，用于验证认证拒绝场景
- `4544 2491 6767 3670`：渠道返回失败，用于验证渠道异常场景
- 独立绑卡（CKO121）成功后 `tr_bank_card_token` 应有对应签约 token 落地

### 路由结果速查矩阵（支付绑卡 / 已绑卡场景）
| preferSign | 核身 Verify | 签约状态 Contract | 签约渠道 Available | 路由结果 Result |
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

**核心规则**：preferSign=Y 且 is3DS=Y 才触发签约；已签约卡走密码 / 免密命中 CKO111；preferSign=N / Null 一律不签约、不走订阅渠道。

---
id: scn_cko_subscription_payment_cases
object_type: Scenario
domain: channel-integration
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: wiki:5b35d40b-b532-44de-b69e-abffc289be85
tags:
- CKO
- 订阅支付
- 测试用例
- 路由矩阵
subdomain: cko
module: subscription-payment
sensitivity: normal
name: CKO订阅支付测试场景集
aliases: []
related_services: []
related_tables:
- tr_bank_account
- tr_bank_card_token
- tr_deduct_channel
- t_deduct_protocol
- t_contract_sign_info
- tt_inst_order
- t_filter_node
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
五大模块测试用例集，覆盖 CKO 订阅支付（CKO101/102/111/121）在不同收银台与业务场景下的路由与状态校验：
- 老收银台（cashdesk = PayBy App）
- 新收银台（cashierii = BotIM，含充值）
- 独立绑卡（wallet→card，固定 CKO121）
- 特殊业务（付款码、代扣、authSign、facepay、国际汇款）
- 回归

## 前置条件
- 测试商户 merchant：200000036054（一般已满足收单鉴权要求）
- 支付鉴权配置由专属人员统一维护，测试人员不可改动；如不满足联系配置负责人
- 核身规则按需在 basis → 风控管理 → 风控事件 → 核身规则管理 添加并提交审核生效（threeds=3DS）
- 测试卡号有效期与 CVV 不校验，按用途选择本地/外卡/借记/贷记/认证拒绝/渠道失败卡
- 全局开关 `cashdesk.alwaysPreferSign` / `cashier.alwaysPreferSign` 按用例需要打开（借记卡强制 preferSign=Y）

## 操作步骤
### 模块一：老收银台（PayBy App，~33+ 用例）
- 充值与收单两类入口
- 卡场景：新卡（quick_pay）/ 已绑未签卡 / 已签约卡
- 维度组合：preferSign（Y / N / Null） × 核身（3DS / 密码 / 免密） × 签约渠道是否可用
- 包含支付并签约、订阅（代扣）支付、异常流程、支付鉴权 + 风控矩阵

### 模块二：新收银台（cashierii / BotIM，~16 用例）
- 标准收银台收单，与老收银台同维度组合
- 异常流程：处理中、失败、风控拒绝、补偿、绑卡限额

### 模块三：独立绑卡（7 用例）
- wallet→card 入口，固定 CKO121
- 带签约绑卡 / 不带签约绑卡
- 解绑、重新绑卡
- 渠道处理中、渠道失败

### 模块四：特殊业务（~24 用例）
- 付款码（payment code）
- PAYPAGE（含匿名支付，不支持订阅，需校验不签约）
- 代扣（AUTODEBIT，使用 authProtocolNo）
- facepay
- authSign
- 国际汇款（remittance）
- 灰度发布（gray release）

### 模块五：回归（11 用例）
- PAYPAGE
- BotIM 扫码
- 代扣（auto-debit）
- Direct Pay
- 收单
- 退款
- 超大扩展字段

### 收单触发参数
| paySceneCode | 场景 | 关键参数/操作 |
|---|---|---|
| DYNQR | 普通收单 | 取 `interActionParams.tokenUrl` 生成二维码，App 扫码进收银台 |
| PAYANDSIGN | 支付并签代扣 | protocolSceneCode=111，落 `t_deduct_protocol.deduct_protocol_no` |
| AUTODEBIT | 代扣 | `authProtocolNo`=协议号，提交后无交互直接完成 |
| PAYPAGE | 匿名支付 | 携带 redirectUrl / customerId / oneTimePayment，浏览器打开 tokenUrl |

## DB 校验点
- **订单**：订单状态 + 实际路由渠道（CKO101 / 102 / 111 / 121）
- **银行卡 / 协议**：
  - `tr_bank_account`（status=1 激活 / 0 解绑 / 3 处理中）
  - `tr_bank_card_token`（是否新增、channel=签约渠道、token=加密协议号、status=Y/N）
  - `tr_deduct_channel`（独立绑卡签约成功后新增）
  - `t_deduct_protocol.deduct_protocol_no`（PAYANDSIGN 后落库，可用于代扣）
  - `t_contract_sign_info.sign_contract_no`（协议号来源之一）
- **CMF**：`tt_inst_order` / `tt_inst_order_result`（扩展字段含渠道返回 signTransactionId、signSource）
- **日志**：各接口 preferSign / frictionless / is3DS 传参；CMF 返回 signTransactionId / signSource
- **风控**：DataEden 校验点（如 CP-GR-000005）、风控画像 threeDSFlag
- **交易查询**：sim.intra.test2pay.com → 综合管理 → 联合查询，订单号类型 product_order_no

## 预期结果
### 路由结果速查矩阵（支付绑卡 / 已绑卡场景）

| preferSign | 核身 | 签约状态 | 签约渠道可用 | 路由结果 |
|---|---|---|---|---|
| Y | 3DS | 新卡 / 未签 | 可用 | CKO102 签约 |
| Y | 3DS | 新卡 / 未签 | 不可用 | CKO101（降级，不签约） |
| Y | 密码 / 免密 | 未签约 | 可用 | 非 CKO102 |
| Y | 3DS | 已签约 | 可用 | CKO101（卡支付） |
| Y | 3DS | 已签约 | 不可用 | CKO102 重签 |
| Y | 密码 / 免密 | 已签约 | 可用 | CKO111 订阅 |
| Y | 密码 / 免密 | 已签约 | 不可用 | 非 CKO111 |
| N / Null | 3DS | 任意 | 可用 | CKO101 |
| N / Null | 密码 | 已签约 | 可用 | 非 CKO111 |

### 关键判定规则
- 仅当 `preferSign=Y` 且 `is3DS=Y` 才触发签约
- 已签约卡走密码 / 免密命中 CKO111（订阅 / 代扣）
- `preferSign=N / Null` 一律不签约、不走订阅渠道
- 独立绑卡固定走 CKO121，不受配置影响
- PAYPAGE（含匿名支付）不支持订阅支付
- 签约成功后收银台收到带 signTransactionId、`signSource=CKO` 的绑卡消息，落 `tr_bank_card_token`

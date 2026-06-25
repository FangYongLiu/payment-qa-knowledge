---
id: scn_cko_subscription_payment
object_type: Scenario
name: CKO 订阅支付测试场景集(路由矩阵 + 渠道定义 + 测试指南)
aliases: [CKO订阅支付测试, CKO渠道定义, CKO路由矩阵]
domain: channel
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/2228977707; wiki:5b35d40b-b532-44de-b69e-abffc289be85; wiki_attachment:af0d55d4-10d6-454b-b0a9-8ff7e104cd04
tags: [cko, subscription, 订阅支付, 路由矩阵, 测试用例, preferSign, 3DS]
related_services: [svc_qpay_cko]
related_tables: [tbl_cashdesk_t_filter_node, tbl_member_tr_bank_account, tbl_member_tr_bank_card_token, tbl_member_tr_deduct_channel]
related_logs: []
---

# CKO 订阅支付测试场景集

## 触发 / 入口
五大模块测试用例集,覆盖 CKO 订阅支付(CKO101/102/111/121)在不同收银台与业务场景下的路由与状态校验:
- 老收银台(cashdesk = PayBy App,~33+ 用例):充值与收单;卡场景=新卡 quick_pay / 已绑未签 / 已签约;维度组合 preferSign(Y/N/Null)×核身(3DS/密码/免密)×签约渠道是否可用;含支付并签约、订阅(代扣)、异常流程、鉴权+风控矩阵。
- 新收银台(cashierii = BotIM,含充值,~16 用例):标准收银台收单,同维度;异常流程(处理中、失败、风控拒绝、补偿、绑卡限额)。
- 独立绑卡(wallet→card,固定 CKO121,7 用例):带/不带签约绑卡、解绑、重绑、渠道处理中/失败;重点校验 Card contract info 与 Card_id 关联(Case No. 1~7)。
- 特殊业务(~24 用例):付款码(payment code)、PAYPAGE(含匿名支付,不支持订阅,需校验不签约)、代扣(AUTODEBIT,用 authProtocolNo)、facepay、authSign、国际汇款、灰度发布。
- 回归(11 用例):PAYPAGE、BotIM 扫码、代扣、Direct Pay、收单、退款、超大扩展字段。

## CKO 渠道角色定义
| 渠道 | 角色 | 核身要求 | 说明 |
|---|---|---|---|
| CKO101 | 支付渠道 Payment | 必须 3DS | 不具备签约能力,仅完成支付;已签约卡走 3DS 也走 CKO101 |
| CKO102 | 签约渠道 Signing | 必须 3DS | 绑卡并同时签约(bind-and-pay while signing) |
| CKO111 | 协议/订阅渠道 Subscription | 非 3DS(密码/免密) | 要求卡上已有有效签约协议;渠道侧 frictionless=Y、is3ds=N |
| CKO121 | 绑卡渠道 Card-binding | 必须 3DS | 独立绑卡 + 签约,固定用于独立绑卡场景,不受配置影响 |

## 关联关系
- **涉及服务**:[[svc_qpay_cko]](= `related_services`)
- **校验的表**:[[tbl_cashdesk_t_filter_node]](= `related_tables`);member.tr_bank_account / tr_bank_card_token / tr_deduct_channel、deduct.t_deduct_protocol、protocol.t_contract_sign_info、cmf.tt_inst_order/tt_inst_result(对象待补)
- **端到端流程**:[[flow_cko_subscription_payment]]

## 前置条件
- 测试商户 merchant:`200000036054`(一般已满足收单鉴权要求);支付鉴权配置由专属人员统一维护,测试人员不可改动。
- 核身规则:basis → 风控管理 → 风控事件 → 核身规则管理添加(事件类型 payment,规则维度 memberId = 本人 mid,核身方式 threeds=3DS,优先级 0),改为生效后经 basis 审核刷缓存生效。
- 测试卡有效期与 CVV 均不校验。
- 全局开关 `cashdesk.alwaysPreferSign` / `cashier.alwaysPreferSign` 按用例需要打开(借记卡强制 preferSign=Y)。

### 测试卡清单
| 卡号 | 类型 |
|---|---|
| 4010 0617 0000 0021 | 本地卡 Debit |
| 5385 3083 6013 5181 | 本地卡 Credit |
| 4659 1055 6905 1157 | 外卡 Debit |
| 4242 4242 4242 4242 | 外卡 Credit |
| 4870 5270 1770 0692 | 认证拒绝 Authentication rejected |
| 4544 2491 6767 3670 | 渠道返回失败 Channel failure(异常用) |

参考 Checkout 官网测试卡:https://www.checkout.com/docs/developer-resources/testing/test-cards

## 操作步骤
### 收单测试入口
- 网关:`http://qa.test2pay.com/manualTest/gateway/sgs`;service:`acquire2/placeOrder`;测试商户 `200000036054`。
- 业务参数通过 `bizContent` 按 `paySceneCode` 区分场景;二维码生成器 `https://cli.im/text`。

| paySceneCode | 场景 | 关键参数 / 操作 |
|---|---|---|
| DYNQR | 普通收单 | 取 `interActionParams.tokenUrl` 生成二维码,App 扫码进收银台 |
| PAYANDSIGN | 支付并签代扣 | protocolSceneCode=111,落 `t_deduct_protocol.deduct_protocol_no` |
| AUTODEBIT | 代扣 | `authProtocolNo`=协议号,提交后无交互直接完成 |
| PAYPAGE | 匿名支付 | 携带 redirectUrl / customerId / oneTimePayment,浏览器打开 tokenUrl |

### 协议号来源
PAYANDSIGN 成功后取 `t_deduct_protocol.deduct_protocol_no`;或取 `t_contract_sign_info.sign_contract_no`。

## DB 校验点
- **订单**:订单状态 + 实际路由渠道(CKO101 / 102 / 111 / 121)。
- **银行卡 / 协议**:
  - `tr_bank_account`(status=1 激活 / 0 解绑 / 3 处理中)。
  - `tr_bank_card_token`(是否新增、channel=签约渠道、token=signTransactionId 加密、status=Y/N);该表有效数据是「卡是否已签约」的判断依据。
  - `tr_deduct_channel`(独立绑卡签约成功后新增)。
  - `t_deduct_protocol.deduct_protocol_no`(PAYANDSIGN 后落库,可用于代扣)。
  - `t_contract_sign_info.sign_contract_no`(协议号来源之一)。
- **CMF**:`tt_inst_order` / `tt_inst_result`(扩展字段含渠道返回 signTransactionId、signSource)。
- **日志**:各接口 preferSign / frictionless / is3DS 传参;CMF 返回 signTransactionId / signSource。
- **风控**:DataEden 校验点(如 CP-GR-000005)、风控画像 threeDSFlag。
- **交易查询**:`http://sim.intra.test2pay.com/basis/login` → 综合管理 → 联合查询,订单号类型 product_order_no(填收单返回的 orderNo)。

## 预期结果
### 路由结果速查矩阵(支付绑卡 / 已绑卡场景)
| preferSign | 核身 | 签约状态 | 签约渠道可用 | 路由结果 |
|---|---|---|---|---|
| Y | 3DS | 新卡 / 未签 | 可用 | CKO102 签约 |
| Y | 3DS | 新卡 / 未签 | 不可用 | CKO101(降级,不签约) |
| Y | 密码 / 免密 | 未签约 | 可用 | 非 CKO102 |
| Y | 3DS | 已签约 | 可用 | CKO101(卡支付) |
| Y | 3DS | 已签约 | 不可用 | CKO102 重签 |
| Y | 密码 / 免密 | 已签约 | 可用 | CKO111 订阅 |
| Y | 密码 / 免密 | 已签约 | 不可用 | 非 CKO111 |
| N / Null | 3DS | 任意 | 可用 | CKO101 |
| N / Null | 密码 | 已签约 | 可用 | 非 CKO111 |

### 关键判定规则
- 仅当 `preferSign=Y` 且 `is3DS=Y` 才触发签约(CKO102)。
- 已签约卡走密码 / 免密命中 CKO111(订阅 / 代扣)。
- `preferSign=N / Null` 一律不签约、不走订阅渠道。
- 独立绑卡固定走 CKO121,不受配置影响。
- PAYPAGE(含匿名支付)不支持订阅支付,不会路由到 CKO111。
- 签约成功后收银台收到带 signTransactionId、`signSource=CKO` 的绑卡消息,落 `tr_bank_card_token`。

### preferSign 来源与取值
满足任一即 preferSign=Y:① 支付鉴权透传([[tbl_cashdesk_t_filter_node]]);② 全局配置 alwaysPreferSign=true 且借记卡时强制 Y。取值:Y 优先签约/订阅;N 明确不签约;Null 未命中按不签约处理。

### 独立绑卡(CKO121)
- 正常卡:CKO121 绑卡成功,`tr_bank_card_token` 落库有效 token,Card contract info 与 Card_id 正确关联。
- 4870 5270 1770 0692(认证拒绝):绑卡失败,无有效 token 落库。
- 绑卡成功后该卡可在后续支付被识别为已签约卡,走对应 CKO 签约渠道(如 CKO111)。
- 7 个用例分别覆盖各卡类型与异常分支,确保 Card_id ↔ Card contract info 关联符合预期。

> 不确定 / 缺失的点标「待补」,留待人工补充。

---
id: api_payby_transfer_bank_card_notify
object_type: API
domain: payby-transfer-to-bank
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: api-docs/payby-transfer-bankcard-v0.2-p3
tags:
- notify
- async
- callback
subdomain: null
module: null
sensitivity: normal
name: 商户转账银行卡成功通知
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
当商户付款到银行卡有结果后,PayBy会把相关结果异步推送给商户,商户需接收处理并返回应答。具体到账时间以银行实际结算时间为准。

注意事项:
1. 同一个通知可能会被多次发送到商户系统,商户系统必须能够正确处理重复通知(幂等)。
2. 后台通知交互中,若PayBy收到的响应不符合规范或超时,会判定通知失败并重发。默认重试7次,时间间隔(分钟):2, 10, 10, 60, 120, 360, 900。但PayBy不保证通知最终成功。
3. 若订单状态不明或未收到支付结果通知,建议商户主动调用转账查询接口确认订单状态。
4. 通知请求带签名,签名算法与普通请求相同。消息由PayBy的RSA私钥签署,商户需使用从商户portal下载的PayBy公钥验证签名。

## 路径/方法
- 方向: PayBy → 商户 (异步回调)
- 协议: HTTP, 由 Http Header + Http Body(JSON) 组成
- 通知地址: 商户在下单时提供的 notifyUrl

## 入参
Http Body (JSON 对象):

| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 转账银行卡订单信息 | transferBankCardOrder | Required | TransferBankCardOrder | - |

签名规则:与普通请求相同,使用 PayBy RSA 私钥签名,商户用 PayBy 公钥验签。

## 出参
商户收到通知后需返回字符串:
- 返回 `SUCCESS` 表示成功接收
- 其他返回值表示异常,PayBy 将按重试策略重发通知

## 错误码
本接口为商户应答,无 PayBy 返回码。商户应答非 `SUCCESS` 视为失败,触发重试(默认7次,间隔 2/10/10/60/120/360/900 分钟)。

## 测试校验点
1. 验签:使用 PayBy 公钥能正确验证通知签名。
2. 幂等:相同通知多次到达,商户业务结果一致,不重复处理。
3. 应答:商户正确返回 `SUCCESS`,PayBy 不再重试;返回非 `SUCCESS` 或超时,按 2/10/10/60/120/360/900 分钟间隔重试,最多 7 次。
4. 通知体结构:`transferBankCardOrder` 字段必填,字段类型符合 TransferBankCardOrder 定义。
5. 状态对账:订单状态不明时,可通过查询转账银行卡接口(getTransferToBankCard)校对最终状态。
6. 到账时间差异:不同银行结算时间不同,以实际到账时间为准。

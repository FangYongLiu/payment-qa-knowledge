---
id: api_payby_protocol_notify
object_type: API
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: upload:c28e6aeb-4485-4713-83f7-c926b25d5235
tags:
- notify
- async
- callback
- protocol
subdomain: null
module: null
sensitivity: normal
name: 签约协议结果通知接口
aliases:
- 签约协议结果通知
related_services:
- svc_protocol
---

## 用途
当协议状态变化为指定状态时，PayBy 异步将结果通知商户系统，商户接收处理并返回应答。

触发的指定状态列表：
1. protocol.applySignStatus == CLOSED
2. protocol.protocolStatus == TERMINATED
3. protocol.protocolStatus == EFFECTIVE

注意事项：
1. 同样的通知可能会多次发送给商户系统，商户系统必须能够正确处理重复通知（幂等）。
2. 若 PayBy 收到的商户应答不符合规范或超时，PayBy 判定本次通知失败并重发，默认重试 7 次，时间间隔(分钟)：2, 10, 10, 60, 120, 360, 900；但不保证最终一定通知成功。

## 路径/方法
- 由商户在【申请签约协议】请求中通过 `notifyUrl` 指定接收地址
- 提交方式：POST（遵循接口规则：HTTPS、JSON、UTF-8、SHA256WithRSA 签名）

## 入参
通知参数（Http Body）：

| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 协议信息 | protocol | Required | Protocol | 协议详情对象 |

Protocol 字段：

| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 商户订单号 | merchantOrderNo | Required | String(64) | |
| PayBy协议号 | authProtocolNo | Optional | String(32) | |
| 申请签约状态 | applySignStatus | Required | String(32) | APPLYING / CLOSED / SIGNED / FAILURE |
| 签约时间 | signTime | Optional | Timestamp(3) | |
| 生效时间 | effectTime | Optional | Timestamp(3) | |
| 失效时间 | invalidTime | Optional | Timestamp(3) | |
| 协议状态 | protocolStatus | Optional | String(32) | EXPIRED / TERMINATED / EFFECTIVE / INEFFECTIVE |
| 签约人ID | signerId | Optional | String(32) | 签约人在 PayBy 的会员 ID |
| 扣除类型 | deductType | Optional | String(32) | SP=Single Pay Method |
| 扩展信息 | extension | Optional | Map<String,String> | 见下 |

extension 扩展信息：
- payMethodType：用户选择的支付方式，BALANCE、CARD_PAY
- lastFour：银行卡后 4 位
- cardBrand：卡组织（VISA / MASTERCARD / CUP / JCB / DINERS / MAESTRO / AE / EBT / DISCOVER / CIRRUS / RUPAY / UATP / ELO）

## 出参
商户收到通知后，返回字符串 `SUCCESS` 表示成功接收，其他值视为异常并触发 PayBy 重试。

## 错误码
本通知接口由 PayBy 主动发起，不定义独立返回码；商户应答仅区分：
- `SUCCESS`：接收成功，PayBy 不再重发
- 其他/超时/不符合规范：判定为通知失败，按重试策略（2,10,10,60,120,360,900 分钟，共 7 次）重发

## 测试校验点
1. 通知仅在以下状态触发：applySignStatus=CLOSED，或 protocolStatus=TERMINATED，或 protocolStatus=EFFECTIVE。
2. 重复通知场景下，商户系统需保证幂等处理。
3. 商户返回非 `SUCCESS` 或超时，验证 PayBy 按 2/10/10/60/120/360/900 分钟间隔重试，最多 7 次。
4. 通知请求需通过 SHA256WithRSA 签名校验，HTTPS + JSON + UTF-8。
5. Protocol 中关键字段（merchantOrderNo、authProtocolNo、applySignStatus、protocolStatus、signTime/effectTime/invalidTime、signerId）正确传递。
6. extension 字段在不同支付方式（BALANCE / CARD_PAY）下的内容（payMethodType、lastFour、cardBrand）符合预期。
7. deductType=SP 等取值正确返回。
8. 校验商户在【申请签约协议】中传入的 notifyUrl 被准确回调。

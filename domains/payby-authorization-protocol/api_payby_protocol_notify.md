---
id: api_payby_protocol_notify
object_type: API
domain: payby-authorization-protocol
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: api-docs/payby-auth-agreement-v1.0.2-p1
tags:
- notify
- callback
- protocol
subdomain: null
module: null
sensitivity: normal
name: 签约协议结果通知
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
当协议状态为指定状态时，PayBy 把相关结果发送给商户，商户需要接收处理并返回应答。

指定状态列表：
1. protocol.applySignStatus == CLOSED
2. protocol.protocolStatus == TERMINATED
3. protocol.protocolStatus == EFFECTIVE

注意事项：
- 同样的通知可能会多次发送给商户系统，商户系统必须能够正确处理重复的通知。
- 后台通知交互时，若 PayBy 收到商户的应答不符合规范或超时，PayBy 判定本次通知失败，重新发送通知，直到成功为止；但 PayBy 不保证通知最终一定能成功。

重试策略（默认）：
- 重试次数：7 次
- 时间间隔（分钟）：2, 10, 10, 60, 120, 360, 900

## 路径/方法
- 通知方向：PayBy → 商户（回调商户在 [[api_payby_apply_protocol]] 申请时传入的 notifyUrl）
- 提交方式：POST（按 PayBy 接口规则：HTTPS、JSON、UTF-8、SHA256WithRSA 签名）

## 入参
通知参数（Http Body）

| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 协议信息 | protocol | Required | Protocol | - |

Protocol 关键字段：
- merchantOrderNo (Required, String(64))：商户订单号
- authProtocolNo (Optional, String(32))：PayBy 协议号
- applySignStatus (Required, String(32))：APPLYING / CLOSED / SIGNED / FAILURE
- signTime / effectTime / invalidTime (Optional, Timestamp(3))
- protocolStatus (Optional, String(32))：EXPIRED / TERMINATED / EFFECTIVE / INEFFECTIVE
- signerId (Optional, String(32))：签约人在 PayBy 的会员 ID
- deductType (Optional, String(32))：例如 SP=Single Pay Method
- extension (Optional, Map<String,String>)：包含 payMethodType（BALANCE / CARD_PAY）、lastFour、cardBrand 等

## 出参
商户收到通知以后，返回 "SUCCESS" 表示成功接收，其他表示异常。

## 错误码
本通知接口由商户实现并应答，无 PayBy 标准返回码列表。
- 应答非 "SUCCESS" 或超时 → 视为通知失败，触发重试（见"用途"中的重试策略）。

## 测试校验点
1. notifyUrl 能正确接收 POST JSON 通知，并按 SHA256WithRSA 校验签名（Sign、Partner-Id 等 Header）。
2. 三类指定状态均能触发通知并被正确处理：
   - applySignStatus = CLOSED
   - protocolStatus = TERMINATED
   - protocolStatus = EFFECTIVE
3. 重复通知幂等处理：同一 merchantOrderNo / authProtocolNo 多次到达不重复变更业务状态。
4. 应答规范：成功处理后返回字符串 "SUCCESS"；其他返回值（含异常、超时）均视为失败。
5. 重试机制验证：商户应答非 SUCCESS 或超时，PayBy 按 2,10,10,60,120,360,900（分钟）共 7 次重试。
6. 字段解析覆盖 Protocol 全字段，含可选字段 deductType、extension（payMethodType、lastFour、cardBrand）。
7. cardBrand 取值兼容性：VISA、MASTERCARD、CUP、JCB、DINERS、MAESTRO、AE、EBT、DISCOVER、CIRRUS、RUPAY、UATP、ELO。
8. 通知失败兜底：商户系统应能通过 [[api_payby_get_protocol]] 主动查询协议状态对账。

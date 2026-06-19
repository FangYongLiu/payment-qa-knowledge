---
id: api_payby_notify_vam_deposit
object_type: API
domain: payby-open-api
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: api-docs/payby-api-v2.25-p17
tags:
- 异步通知
- VAM
- 充值
subdomain: async-notification
module: null
sensitivity: normal
name: VAM充值通知接口
aliases:
- VAM充值通知
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
发生VAM充值时，PayBy将相关充值信息以数据流形式异步推送给商户，商户接收处理后按规范返回应答。

注意：
1. 同样的通知可能会多次发送给商户系统，商户系统必须能够正确处理重复的通知。
2. 后台通知交互时，如果PayBy收到商户的应答不符合规范或超时，PayBy会判定本次通知失败，并重新发送通知，直到成功为止（默认重试7次，时间间隔：2, 10, 10, 60, 120, 360, 900，单位：分钟），但PayBy不保证通知最终一定能成功。
3. 在订单状态不明或者没有收到PayBy支付结果通知的情况下，建议商户主动调用查订单接口确认订单状态。

## 路径/方法
由PayBy向商户预先配置的回调地址发起的异步HTTP通知（POST，application/json; charset=UTF-8）。原文未给出具体URL路径。

## 入参
通知参数（Http Body 中核心字段）：

| 字段名 | 变量名 | 必填 | 类型 | 描述 |
| --- | --- | --- | --- | --- |
| 拒付订单（VAM充值订单） | vamDepositOrder | Required | VamDepositOrder | VAM充值订单信息 |

通知样例字段：
- `notify_time`：通知时间（如 `20241224061738`）
- `notify_timestamp`：通知时间戳（如 `1735006658869`）
- `notify_id`：通知唯一编号（如 `202409300013926551`）
- `_input_charset`：字符集（`UTF-8`）
- `vamDepositOrder`：
  - `remitterInfo`：汇款人信息（示例 `MR HUA JIANG`）
  - `amount.amount`：金额（示例 `3000`）
  - `amount.currency`：币种（示例 `AED`）
  - `orderNo`：PayBy订单号（示例 `131727701521486397`）
  - `referenceNo`：参考号（示例 `UFOC0HQ008`）
  - `senderBankCode`：付款方银行代码（示例 `BBMEAEADXXX`）
  - `depositDetails`：充值明细（示例 `REF AEV260832YLQ4K5D FIS ...`）
  - `transactionTime`：交易时间戳（示例 `1727701521000`）
  - `status`：状态（示例 `SUCCESS`）

Http Header 示例：`Content-Type: application/json; charset=UTF-8`

## 出参
商户收到通知后必须返回：
```
{"response":"SUCCESS"}
```
返回该值表示成功接收，其他值表示异常，PayBy将按重试策略再次推送。

## 错误码
原文未在本接口下定义专用错误码。商户应答非 `{"response":"SUCCESS"}` 或超时即视为通知失败，触发重试（默认7次，间隔 2, 10, 10, 60, 120, 360, 900 分钟）。

## 测试校验点
1. 通知幂等性：相同 `notify_id` / `orderNo` 多次推送时，商户系统不应重复入账。
2. 应答格式：仅当返回 `{"response":"SUCCESS"}` 时PayBy停止重试；其他响应或超时应触发重试。
3. 重试策略验证：在商户故意返回非SUCCESS或超时场景下，验证重试次数（7次）与时间间隔（2, 10, 10, 60, 120, 360, 900 分钟）。
4. 字段完整性：校验 `vamDepositOrder` 中 `orderNo`、`referenceNo`、`amount.amount`、`amount.currency`、`status`、`transactionTime`、`remitterInfo`、`senderBankCode`、`depositDetails` 是否齐全且类型正确。
5. 金额与币种：`amount.amount` 单位与 `amount.currency`（如 `AED`）一致性校验。
6. 状态字段：`status=SUCCESS` 时入账；其他状态需按业务约定处理。
7. 与查询接口对账：在未收到通知或状态不明时，应通过查订单接口主动核对，避免漏单。
8. 字符集：通知 `Content-Type` 为 `application/json; charset=UTF-8`，`_input_charset=UTF-8`，需按UTF-8解析。

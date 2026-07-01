---
id: scn_pix_wechat_vendor_api
object_type: Scenario
name: PIX 微信 MPC Vendor API 清单、配置与字段校验
aliases: [微信Vendor API, pix-wechat API catalog, 微信渠道配置]
domain: payment-tool
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:PMDPayment/433881954
tags: [pix, wechat, mpc, vendor-api, 配置, 字段校验]
related_services: []
related_tables: []
related_logs: []
---

# PIX 微信 MPC Vendor API 清单、配置与字段校验

## 触发 / 入口
微信 MPC 渠道接入中各业务场景与 Vendor API(Requester / Responder)的对应关系、接入配置项与关键字段含义,作为测试时定位接口、字段与配置的参考。端到端流程见 [[flow_pix_wechat_mpc_payment]] / [[flow_pix_wechat_refund]] / [[flow_pix_wechat_reconciliation]]。

## 关联关系
- **涉及服务**:pix / pix-wechat、wallet、remittance、basis-customer、tradeii、bill、reconciliation、vendor(Tenpay)(服务对象待补)
- **关键表 / 存储**:ES(商户码信息含费率)(对象待补)

## Vendor API 场景与角色映射
| 场景 | 微信 Vendor API | 角色 |
|---|---|---|
| 解析二维码 | `/pix/mpc/v1/parse`(QUERY_MERCHANT_CODE) | Requester |
| 创建交易/扫码支付 | `/pix/mpc/v1/create-trade`(SCAN_CODE_FOR_PAYMENT) | Requester |
| 处理交易结果 | NOTIFY_PAYMENT_RESULT | Requester |
| 退款 | REFUND | Responder |
| 关闭支付 | CLOSE_PAYMENT | Responder |
| 查询支付 | QUERY_PAYMENT_ORDER_INFO | Responder |
| 查询退款 | QUERY_REFUND_ORDER_INFO | Responder |
| 下载对账文件 | QUERY_BILL_ADDRESS | Requester |
| 通知最终支付结果 | NOTIFY_FINAL_PAYMENT_RESULT | Responder |
| 退款推定通知 | NOTIFY_PRESUPPTIVE_REFUND_SUCCESS | Responder |

## 接入配置项(UAT / PROD 各维护一套)
| Item | 字段 | 说明 |
|---|---|---|
| Account institution identifier | `PyerAcctIssrId` | 付款方账户机构标识 |
| Acquirer institution identifier | `PyeeAcctIssrId` | 收单机构标识 |
| Mobile application identifier | `AppId` | 移动应用标识 |
> 具体取值由对接方部署时填入(待补)。

## 字段含义与 Q&A
### SCAN_CODE_FOR_PAYMENT(`/pix/mpc/v1/create-trade`)
- `PyerTrxTrmNo`:Payer terminal code,即 Device Id。
- `BizTp`:Business type,来自 `QUERY_MERCHANT_CODE`。
- `TrxDtTm`:交易日期,须与 `TrxId` 中日期一致。
- `ClbckUrl`:账户机构回调收单机构 URL(待确认)。
- `PrmtInf`:营销信息(待确认)。

### NOTIFY_PAYMENT_RESULT
- 可能返回失败结果(会收到 failure);trade close / failure 都会通过此接口通知。
- `instOrderNo` 来自 tradeii(关键字 `DbtrBankId`)。

### QUERY_PAYMENT_ORDER_INFO
- `PyerIDTp` / `PyerIDNo`:是否必填待确认(TODO)。

### REFUND
- 仅同步响应,无异步通知;微信 10 分钟内通过 `QUERY_REFUND_ORDER_INFO` 查询;超时触发 `NOTIFY_PRESUPPTIVE_REFUND_SUCCESS` 推定;允许退款失败。
- 退款金额:`Refund pay amount = Refund transaction amount / Original transaction amount × Original pay amount`。

### NOTIFY_PRESUPPTIVE_REFUND_SUCCESS
- 多次查询且超 10 分钟无结果时推定退款成功;默认仅推定 1 次;一旦推定按成功推进;钱包次日账单获得记录。

## 汇率同步与计费(Rate Sync)
- 基础汇率来源 remittance(AED→当地币种),pix 通过 dubbo api 周期同步;Rate Margin Percent 按渠道配置;basis-customer 提供查询/配置 UI。
- Customer Rate = Exchange Rate × (1 − Margin Percent);Pay Amount = Transaction Amount / Customer Rate。
- 设计参考 pix-SD-FX Rate;Round/Ceiling 进位规则与利润口径 TODO。

## DB 校验点
- ES 中商户码信息(含费率)是否在 parseCode 阶段正确落库。
- 创建交易金额是否按 rate config 校验一致。
- 退款金额换算、推定退款的账单落地。

## 预期结果
- 各 Vendor API 按角色(Requester/Responder)正确实现并通过沙箱验证。
- 关键字段(PyerTrxTrmNo / BizTp / TrxDtTm / ClbckUrl)取值与来源符合定义。
- 配置项在 UAT / PROD 分别正确注入。
> 标 TODO / 待确认的字段需人工补充。

---
id: domain_merchant_acquisition
object_type: Domain
domain: merchant-acquisition-testing
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:4ef3640b-38b5-4756-81d5-d729c241dc79
tags:
- acquiring
- payment
- qa
subdomain: null
module: null
sensitivity: normal
name: 商户收单
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述

商户收单业务域覆盖商户接入支付中台后的全链路交易流程，包括下单、支付、预授权、撤销、退款、对账等关键能力。其测试方法论的核心理念是：**不只测商户接口本身，而要验证支付中台各服务的调用链 + 数据库落库 + 资金流 + 通知 + 对账这一整条链路**。一笔成功的接口响应只是测试的起点，不是终点。

域内统一遵循"五段式 E2E 验证骨架"作为方法论基线，所有场景手册（§5.x）均依赖该骨架、用例分类、命名规范。

## 覆盖范围

本域覆盖商户收单业务全链路，包括但不限于：

- **下单**：PAYPAGE、DIRECTPAY 等支付场景的 placeOrder
- **支付**：含 Local / International 卡，MasterCard / Visa，ApplePay / GooglePay / SamsungPay 等多支付方式；DCC（动态币种转换）
- **预授权（PreAuth）**：mpgs apiOperation=AUTHORIZE，仅冻结不扣款，默认 7 天有效期，不进 Fund Flow、不进对账单
- **Capture**：PreAuth 之后真扣款，产生入账分录，进对账单
- **Refund**：全额 / 部分退款，反向资金流
- **Void / Revoke（撤销）**：PreAuth 撤销不产生 Fund Flow；普通撤销在对账单中显示为 REVERTED
- **对账**：T+1 日对账单 ZIP，包含 Transaction / Settlement / Fund Statement 三类 CSV
- **异步通知（notifyUrl）**：最多 7 次重试，约 24 小时窗口

环境覆盖 SIM / UAT / 生产，UAT 域名为 `https://uat.test2pay.com`，生产域名仍为 `https://api.payby.com`（品牌切换中）。

## 关键服务/流程

**典型服务调用链（按场景）**：

| 场景 | 调用链 |
|---|---|
| PAYPAGE 下单 | sgs → acquireii → cashierii → authPay → cmf → router → mpgs |
| DIRECTPAY 下单 | sgs → acquireii → tradeii → ppcenter / pfs-payment → payment → cmf → router → mpgs |
| PREAUTH | sgs → acquireii → cashierii → authPay → cmf → router → mpgs（apiOperation=AUTHORIZE） |
| CAPTURE | sgs → acquireii → tradeii → ppcenter → pfs-payment → payment → cmf → router → mpgs |
| Refund | sgs → acquireii → tradeii → cmf → router → mpgs |

**核心数据库与表**（高频核对）：

- `acquireii`：t_acquire_order、t_payment_info、t_preauth_control、t_card_info、t_refund_order
- `tradeii`：t_trade_order、t_trade_party、t_pay_order、t_refund_order
- `cmf`：tt_cmf_order、tt_inst_order、tt_inst_order_result
- `payment`：tb_biz_payment_order、tb_payment_order
- `reconciliation`：t_fund_flow、t_clear_flow、t_bill_summary
- `ppcenter`：t_product_apply_order
- `pbsdb`：tb_pbs_price_cal
- `commission`：t_comm_detail
- `member`：tr_bank_account

**核心资金账户**：

- Fund-In Pending Settlement / Fund-In Pending Clearing
- Merchant Pending for Clearing / Merchant Basic
- Payby Revenue
- Refund Pending for Clearing
- DCC MarkUp Revenue / CKO DCC FX Gain/Loss

**关键流程接口**：

- `/sgs/api/acquire2/placeOrder`：下单
- `/sgs/api/acquire2/refund/placeOrder`：退款
- `/sgs/api/acquire2/download/getOrderStatement`：对账单下载
- `/sgs/api/member/getBalance`：余额查询

## QA 关注点

**五段式 E2E 验证（缺一不可）**：

1. **接口响应**：HTTP 状态码、`head.applyStatus`、`head.code`、业务字段（orderNo / status / interactionParams.tokenUrl）。注意 `applyStatus=SUCCESS` ≠ 业务成功，需看 code 与 status。
2. **服务调用链**：按 traceCode 全链路查日志，确认每个服务都打到、关键参数正确（如 PreAuth 的 mpgs 请求必须是 AUTHORIZE 而非 PAY），无 5xx / 重试堆叠 / 超时。
3. **数据库落库**：表存在性、记录数量、状态字段、金额字段、跨表关联（merchantOrderNo / paymentSeqNo / preauthOrderNo）一致。
4. **Fund Flow**：借贷平衡（Total Dr = Total Cr）、方向正确、金额一致。**特别注意 PreAuth 不产生 Fund Flow，Capture 才产生**——这是新 QA 高频踩坑点。
5. **通知 & 对账**：notifyUrl 触发与 body 校验，商户回 `{"response":"SUCCESS"}` 后不再重试；T+1 对账单包含本笔（PreAuth 除外）。

**用例骨架 A/B/C/D/E**（每个场景至少覆盖 5 类）：

- A 正向流程（不同卡品牌、金额段、saveCard、异步通知）
- B 异常流程（参数缺失、API 超时、外部渠道错误用 expiry 模拟、风控拒绝、幂等冲突）
- C 数据一致性（落库、Fund Flow 平衡、跨表关联、对账单一致）
- D 边界与并发（金额边界、时间戳 ±15 分钟、跨日订单、长字符串）
- E 权限与安全（62026 PRODUCT_IS_NOT_APPLIED、Invalid partner id、403 UNAUTHORIZED、REQUESTTIME_TOO_EARLY/LATER、IP 白名单）

**测试数据规范**：

- merchantOrderNo 命名：`QA_<场景>_<时间戳>_<可选标记>`，便于清洗和排查
- 关键金额：0（错误码）、0.01（精度）、499.99 / 500（密码验证边界）、1,000,000（风控限额）、9,999,999.99（decimal(12,2) 上限）
- MPGS 模拟 expiry：01/39 APPROVED、05/39 DECLINED、04/27 EXPIRED_CARD、08/28 TIMED_OUT、01/37 ACQUIRER_SYSTEM_ERROR、02/37 UNSPECIFIED_FAILURE、05/37 UNKNOWN

**高频错误码**：0

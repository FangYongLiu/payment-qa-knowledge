---
title: 五段式E2E验证骨架
domain: merchant-acquisition-testing
kind: wiki_page
slug: merchant-acquisition-e2e-five-stage-verification
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2125922317
tags: []
---

# 五段式E2E验证骨架详解

商户收单测试的核心方法论：**一笔成功的接口响应只是测试的起点，不是终点**。一笔交易必须从接口响应一路验到对账单，按 ①接口响应 → ②服务调用链 → ③数据库落库 → ④资金流 → ⑤通知与对账 这 5 段串行验证，缺一不可。这套骨架来自实际线上事故复盘——只测前几段不测后几段，错误才会逃逸到生产，让"商户报已付款但订单未支付"、"对账不平"、"清算流水缺失"这类问题暴露。

本页逐段拆解 5 个验证段的核对要点和高频踩坑。详细用例分组见 [[merchant-acquisition-test-case-skeleton-abcde]]。

## 总览：五段链路

```
① 接口响应（API Response）
       │
       ▼
② 服务调用链（Service Log）
       │
       ▼
③ 数据库落库（DB Persistence）
       │
       ▼
④ Fund Flow（资金流）
       │
       ▼
⑤ 通知 & 对账（Notify & Statement）
```

所有场景手册都按这 5 段验证，缺一不可。

## 段 ①：接口响应（API Response）

**该看什么**：

- HTTP 状态码（200 / 4xx / 5xx）
- `head.applyStatus`（`SUCCESS` / `FAIL` / `ERROR`）
- `head.code`（`0` 表示成功，错误码见 [[merchant-acquisition-error-code-quickref]] / [[merchant-acquisition-error-code-cheatsheet]]）
- `body` 业务字段：`orderNo`、`status`、`interactionParams.tokenUrl` 等

**典型期望**：

- 正向：`applyStatus=SUCCESS, code=0, body.acquireOrder.status=CREATED/PAID_SUCCESS/AUTHORIZATION`
- 异常：`applyStatus` 仍可能是 `SUCCESS`，但 `code` 为业务错误码（如 `62026 PRODUCT_IS_NOT_APPLIED`）

**踩坑提醒**：

- ⚠️ `applyStatus = SUCCESS` **≠ 业务成功**。`SUCCESS` 只表示 HTTP 通信成功，业务结果看 `code` 和 `status`。**不要只看 applyStatus**。
- 状态可能是中间态，需要轮询：`CREATED` 状态商户应每 2-6 秒查一次。

## 段 ②：服务调用链（Service Log）

**新 QA 最容易跳过的一段**。一笔交易经过的服务链按场景不同会变：

| 场景 | 典型调用链 |
|---|---|
| PAYPAGE 下单 | sgs → acquireii → cashierii → authPay → cmf → router → mpgs |
| DIRECTPAY 下单 | sgs → acquireii → tradeii → ppcenter / pfs-payment → payment → cmf → router → mpgs |
| PREAUTH | sgs → acquireii → cashierii → authPay → cmf → router → mpgs（mpgs 请求是 `authorize` 不是 `pay`） |
| CAPTURE | sgs → acquireii → tradeii → ppcenter → pfs-payment → payment → cmf → router → mpgs |
| Refund | sgs → acquireii → tradeii → cmf → router → mpgs |

**该看什么**：

- 每个服务都有日志（**没有日志 = 没调到 = 流量没走通**）
- 关键参数符合预期：PreAuth 的 mpgs 请求必须是 `authorize`，不能是 `pay`；DCC 走 CKO123 查汇率、CKO302 实际扣款
- 没有 5xx、没有重试堆叠、没有超时

**实操工具**：

- 在测试平台（如 Kibana）按响应 head 里的 `traceCode` 全链路查
- 或直接登跳板机看应用 log
- 工具入口见 [[merchant-acquisition-test-environment-and-tools]]

**典型核对清单（PreAuth 举例）**：

```
✓ acquireii log: 收到 placeOrder 请求，paySceneCode=PREAUTH
✓ cashierii log: 收银台路由命中
✓ authPay log: 鉴权方案命中、风控通过
✓ cmf log: 选中渠道 MPGS101（按卡品牌+地域）
✓ router log: 路由到 qpay-mpgs
✓ qpay-mpgs log: 向 MPGS 发送的请求 apiOperation = 'AUTHORIZE'  ← 不是 PAY
✓ mpgs response: 成功
```

## 段 ③：数据库落库（DB Persistence）

商户收单 QA 的"硬功夫"。每个场景都有"该增加/更新哪些表、各加几条"的明确预期。

**核心校验维度**：

- **表存在性**：该有记录的表都有，该没记录的表确实没有
- **记录数量**：每张表新增/更新的行数符合预期（不能多也不能少）
- **状态字段**：`status` 值符合状态机
- **金额字段**：`totalAmount` / `dccAmount` / capture amount 等数值正确
- **关联字段**：跨表外键（`merchantOrderNo` / `paymentSeqNo` / `preauthOrderNo`）一致

**高频核对的表速查**：

| 库 | 表 | 用途 |
|---|---|---|
| acquireii | t_acquire_order | 收单订单主表 |
| acquireii | t_payment_info | 支付信息扩展 |
| acquireii | t_preauth_control | 预授权控制（PreAuth 专属） |
| acquireii | t_card_info | 卡信息 |
| acquireii | t_refund_order | 退款订单 |
| tradeii | t_trade_order | 交易订单 |
| tradeii | t_trade_party | 交易参与方 |
| tradeii | t_pay_order | 支付指令 |
| tradeii | t_refund_order | 退款指令 |
| cmf | tt_cmf_order | 渠道订单 |
| cmf | tt_inst_order | 机构订单 |
| cmf | tt_inst_order_result | 机构订单结果 |
| payment | tb_biz_payment_order | 业务支付订单 |
| payment | tb_payment_order | 支付引擎订单 |
| reconciliation | t_fund_flow | 入账流水 |
| reconciliation | t_clear_flow | 清算流水 |
| reconciliation | t_bill_summary | 对账汇总 |
| ppcenter | t_product_apply_order | 产品包申请单 |
| pbsdb | tb_pbs_price_cal | 算费规则 |
| commission | t_comm_detail | 返佣明细 |
| member | tr_bank_account | 会员卡账户 |

**通用 SQL 串联模板**（用 `merchantOrderNo` 串整条链路）：

```sql
-- ① 收单订单
SELECT * FROM acquireii.t_acquire_order WHERE merchant_order_no = 'QA_xxx';
-- ② 交易订单（拿到 trade_order_no 继续）
SELECT * FROM tradeii.t_trade_order   WHERE merchant_order_no = 'QA_xxx';
-- ③ 渠道订单
SELECT * FROM cmf.tt_cmf_order        WHERE order_no = '<acquire_order_no>';
-- ④ 渠道机构订单
SELECT * FROM cmf.tt_inst_order       WHERE cmf_order_no = '<cmf_order_no>';
-- ⑤ 入账流水
SELECT * FROM reconciliation.t_fund_flow WHERE payment_seq_no = '<payment_seq_no>';
```

**建议固化**：每个场景手册都列出"该场景下应增加的具体表+条数"清单，跑用例时逐条核对。

## 段 ④：Fund Flow（资金流）

校验交易资金在 reconciliation 等库中正确生成入账流水、清算流水，金额、方向、币种、参与方账户均符合预期，无缺失或重复。

## 段 ⑤：通知 & 对账（Notify & Statement）

校验异步通知正确推送给商户、对账单（bill summary）正确生成且金额能对平，确保业务侧与平台侧账目一致。

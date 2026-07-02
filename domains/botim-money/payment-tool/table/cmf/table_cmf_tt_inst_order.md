---
id: tbl_cmf_tt_inst_order
object_type: Table
domain: payment-tool
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:AQ/2049867832
tags:
- cmf
- channel-order
- zand
subdomain: cmf-router
module: null
sensitivity: normal
name: CMF渠道订单表 tt_inst_order
aliases:
- tt_inst_order
related_services:
- svc_cmf
---

## 用途
CMF Router 写入的渠道订单表，记录 Fundout 通过 ZAND 各渠道(ZAND201/203/204/207/210)路由后的渠道侧订单实例。是 SP/SQ/VS 流程在 CMF 侧的主订单记录，与 `tt_inst_order_result`(SP/SQ/VS 结果表) 通过 `INST_ORDER_NO` 关联。

数据库：`cmf`。

## 关键列
- `INST_ORDER_NO`：CMF 渠道订单号，格式 `ZAND` + 渠道号 + 序列，例：`ZAND20326031611337631`。与 `tt_inst_order_result.INST_ORDER_NO` 关联。
- `FUND_CHANNEL_CODE`：资金渠道编码，取值 `ZAND201`(域内 AED API)、`ZAND203`(国际 SWIFT USD)、`ZAND204`(结算域内)、`ZAND207`(结算国际)、`ZAND210`(商户门户域内)。
- `STATUS`：渠道订单状态：`I` (In Process)、`S` (Success)、`F` (Failed)、`U` (Unknown)。
- `CURRENCY`：币种(AED / USD)。
- `AMOUNT`：渠道订单金额。
- `RETRY_TIMES`：SQ 轮询重试次数。规则：SP 后约 2 分钟内首轮 → 间隔逐步加大 → `RETRY_TIMES > 35` 进入小时级 → `RETRY_TIMES = 54` 停止轮询。
- `GMT_CREATE`：创建时间。

## 主键/索引
原文未列出主键 DDL；查询习惯：
- 按 `FUND_CHANNEL_CODE` + `GMT_CREATE DESC` 拉取近期渠道订单。
- 按 `INST_ORDER_NO` 关联 `tt_inst_order_result` 取 SP/SQ/VS 明细。

## 校验点(QA 关注)
- 路由正确性：域内 AED → `FUND_CHANNEL_CODE=ZAND201`；国际 SWIFT USD → `ZAND203`；结算域内/国际 → `ZAND204` / `ZAND207`；商户门户域内 → `ZAND210`。错路由(如本应 `ZAND203` 路由到 `TEST201`)需检查 partner routing 配置。
- 状态推进：SP 后 `STATUS=I`；域内 VS 回调后 → `S`；国际经 SQ 轮询 + VS 后 → `S`。VS 已收但仍停在 `I`，排查 `router.t_channel_result_code` 映射(`PROCESSED` 是否映射 `result_status=S`)。
- 与 `t_fundout_order` 一致性：当 `t_fundout_order.unity_result_code = cmf.route.fail` 时，该订单不会落入 `tt_inst_order`(订单创建但未进入 CMF)。
- `RETRY_TIMES` 边界：达到 54 停止 SQ 轮询；测试 SQ 流程或排查"SP 接受但 VS 不到"时关注此字段，必要时 Mock VS 或重置 retries。
- 金额/币种校验：`AMOUNT` / `CURRENCY` 需与 `t_fundout_bankcard_order.fundout_amount` / `fundout_crcy_code` 一致。
- 验证查询：
  ```sql
  SELECT INST_ORDER_NO, FUND_CHANNEL_CODE, STATUS, CURRENCY, AMOUNT, GMT_CREATE
  FROM cmf.tt_inst_order
  WHERE FUND_CHANNEL_CODE = '<channel>' ORDER BY GMT_CREATE DESC LIMIT 5;
  ```

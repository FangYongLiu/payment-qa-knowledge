---
id: tbl_cmf_tt_inst_order
object_type: Table
domain: fund-out-transfer
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:7f334321-3b49-4c87-b6d9-8949925a962a
tags:
- cmf
- channel-order
subdomain: cmf
module: null
sensitivity: normal
name: CMF渠道指令订单表 tt_inst_order
aliases: []
related_services: []
related_tables:
- tbl_cmf_tt_inst_order_result
- tbl_mhtfundout_t_fundout_order
- tbl_router_t_channel_result_code
related_scenarios:
- scn_zand_fundout_test_cases
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
位于 `cmf` 库，用于记录 CMF Router 路由到具体银行渠道（ZAND201/203/204/207/210 等）后产生的渠道指令订单。Fundout Service 创建订单后经 Kafka 投递到 CMF Router，由 Router 在该表创建一条渠道侧订单记录，承载渠道编码、币种、金额、状态及 SQ 轮询次数等信息，是定位渠道层问题的关键表。

## 关键列
| 列 | 说明 |
|---|---|
| INST_ORDER_NO | CMF 渠道订单号，格式为 `ZAND` + 渠道号 + 序列，如 `ZAND20326031611337631`，与 `tt_inst_order_result` 关联 |
| FUND_CHANNEL_CODE | 渠道编码：ZAND201（境内 AED）/ ZAND203（SWIFT USD）/ ZAND204（结算境内）/ ZAND207（结算国际）/ ZAND210（商户门户境内） |
| STATUS | 渠道订单状态：`I` In Process / `S` Success / `F` Failed / `U` Unknown |
| CURRENCY | 出款币种（AED / USD 等） |
| AMOUNT | 出款金额 |
| RETRY_TIMES | SQ 轮询计数；> 35 时间隔变长（小时级），= 54 时停止轮询 |
| GMT_CREATE | 创建时间，用于按时间倒序定位最新订单 |

## 主键/索引
- 主键：`INST_ORDER_NO`（唯一标识渠道指令订单）
- 常用查询：`FUND_CHANNEL_CODE` + `GMT_CREATE DESC`（按渠道查最新单）
- 关联键：`INST_ORDER_NO` ↔ `tt_inst_order_result.INST_ORDER_NO`

## 校验点(QA 关注)
- **路由正确性**：`FUND_CHANNEL_CODE` 应与业务场景一致；若期望 ZAND203 却落到 TEST201，说明 partner routing 配置异常。
- **订单创建**：若 `t_fundout_order.unity_result_code = cmf.route.fail`，则 `tt_inst_order` 中无对应记录，需查 Kibana 与路由配置。
- **状态流转**：
  - 境内 ZAND201/210：SP 后约 12s 内 STATUS 应由 `I` → `S`
  - 国际 ZAND203/207：SP 后保持 `I`，需 SQ 轮询 + VS 回调最终置 `S`
- **STATUS 卡 I**：VS 已到但 STATUS 仍为 `I`，通常是 `router.t_channel_result_code` 未将 PROCESSED 映射为 `result_status=S`。
- **RETRY_TIMES 监控**：
  - 仅国际订单递增；> 50 接近终止阈值，VS 仍未到需触发 Mock VS 或联系 Zand
  - 达到 54 即停止 SQ 轮询，订单不会再自动推进
- **金额/币种一致性**：`AMOUNT`、`CURRENCY` 应与 `t_fundout_bankcard_order.fundout_amount` / `fundout_crcy_code` 一致。
- **订单号格式**：`INST_ORDER_NO` 必须以 `ZAND` + 渠道号开头，便于按渠道筛查。
- **关联校验**：每条 `tt_inst_order` 应在 `tt_inst_order_result` 中有 SP 行；国际单还需 SQ 行；最终需有 VS 行（INST_STATUS=S）。

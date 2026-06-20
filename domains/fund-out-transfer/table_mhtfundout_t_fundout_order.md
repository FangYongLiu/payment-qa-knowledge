---
id: tbl_mhtfundout_t_fundout_order
object_type: Table
domain: fund-out-transfer
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:7f334321-3b49-4c87-b6d9-8949925a962a
tags:
- mhtfundout
- fundout
- order
subdomain: null
module: mhtfundout
sensitivity: normal
name: 出款订单主表 t_fundout_order
aliases:
- t_fundout_order
related_services: []
related_tables:
- tbl_mhtfundout_t_fundout_bankcard_order
- tbl_cmf_tt_inst_order
- tbl_cmf_tt_inst_order_result
related_scenarios:
- scn_zand_fundout_test_cases
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
位于 `mhtfundout` 库，是 Fundout 业务的主订单表。Fundout Service 在创建出款订单时写入该表，记录订单的整体生命周期与状态，是 ZAND 渠道（ZAND201/203/204/207/210）出款流程从下单到最终结果（SUCCESS/FAILURE）的核心数据载体。下游 CMF Router、DPM Accounting 流程围绕该表的订单进行路由、扣款与对账。

## 关键列
- `global_id`：Fundout 订单 ID，18 位数字（示例 `131773657853407506`），用于跨表关联与排序定位最新订单。
- `partner_id`：商户/用户 partner ID（如 `200000080798`、`200000086193`、`200000079033`），用于按账户筛查订单。
- `status`：订单状态，取值 `CREATED`、`PLACED`、`SUCCESS`、`FAILURE`。
- `product_code`：产品码：
  - `220401` 国内转账（ZAND201）
  - `220402` 国际 SWIFT 转账（ZAND203）
  - `230602` 结算/商户提现（ZAND204、ZAND207、ZAND210）
- `created_time`：订单创建时间。
- `unity_result_code`：统一结果码，路由失败时会出现 `cmf.route.fail`，用于排障。

## 主键/索引
- 主键：`global_id`（18 位订单号，按其 DESC 排序取最近订单）。
- 常用查询条件：`partner_id`（按商户拉取订单列表）。
- 原文未列出其他索引信息。

## 校验点(QA 关注)
- 国内转账（ZAND201/210）下单后约 12~15 秒，`status` 应变为 `SUCCESS`，对应 CMF 的 `FUND_CHANNEL_CODE` 与产品码一致。
- 国际 SWIFT（ZAND203/207）需经 SP→SQ→VS，VS 回调到达后 `status` 才会终态化为 `SUCCESS`。
- `product_code` 与实际路由的渠道一致：`220401↔ZAND201`、`220402↔ZAND203`、`230602↔ZAND204/207/210`；若路由到 `TEST201` 等异常渠道需排查 partner 路由配置。
- `unity_result_code = cmf.route.fail`：表示订单已创建但未进入 CMF，需检查 Kibana 日志与路由配置。
- 标准查询：
  ```
  SELECT global_id, status, product_code, created_time, unity_result_code
  FROM mhtfundout.t_fundout_order
  WHERE partner_id = '<partner_id>' ORDER BY global_id DESC LIMIT 5;
  ```
- 与 `t_fundout_bankcard_order`（金额/币种/网络/汇率明细）以及 CMF 的 `tt_inst_order`、`tt_inst_order_result` 关联校验，确保订单金额、渠道、SP/SQ/VS 状态一致。

---
id: tbl_mhtfundout_t_fundout_order
object_type: Table
domain: fund-out-transfer
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:AQ/2049867832
tags:
- mhtfundout
- fundout
- order
subdomain: mhtfundout
module: null
sensitivity: normal
name: Fundout订单主表 t_fundout_order
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
位于 `mhtfundout` 库，是 Fundout 业务的**订单主表**，用于记录由 Fundout Service 创建的出款订单（包括商户门户提现、API 转账、结算出款、个人 App 提现等场景）。每一笔出款请求在 Fundout Service 落库时生成一条记录，作为后续 Kafka 派发、CMF 路由、SP/SQ/VS 流转的源头。

与 `t_fundout_bankcard_order`（银行卡明细）配合使用：主表存订单主键与状态，明细表存币种/金额/网络/汇率等银行卡相关字段。

## 关键列
| 列名 | 说明 |
|---|---|
| `global_id` | Fundout 订单 ID，18 位数字（如 `131773657853407506`），全局唯一标识 |
| `partner_id` | 商户/合作方 ID（如 `200000080798`、`200000086193`、`200000079033`） |
| `status` | 订单状态：`CREATED` / `PLACED` / `SUCCESS` / `FAILURE` |
| `product_code` | 产品码：`220401`（域内转银行 ZAND201）、`220402`（国际 SWIFT ZAND203）、`230602`（结算/商户提现 ZAND204/207/210） |
| `created_time` | 订单创建时间 |
| `unity_result_code` | 统一结果码，路由失败时会出现 `cmf.route.fail` 等值，用于排查 |

## 主键/索引
- 主键：`global_id`（18 位数字订单号）
- 常用查询维度：`partner_id` + `global_id DESC`（按商户取最新订单）

## 校验点(QA 关注)
1. **状态流转**：订单从 `CREATED` -> `PLACED` -> 最终 `SUCCESS` 或 `FAILURE`；域内（ZAND201/210）应在 ~12s 内到达 `SUCCESS`，国际（ZAND203/207）需 SQ 轮询 + VS 回调后才置终态。
2. **product_code 与渠道一致性**：
   - `220401` 应路由到 ZAND201
   - `220402` 应路由到 ZAND203（验证不可错路由到 TEST201）
   - `230602` 应路由到 ZAND204 / ZAND207 / ZAND210
3. **unity_result_code 排查**：当订单创建后在 CMF 找不到对应 `tt_inst_order` 时，检查 `unity_result_code = cmf.route.fail`，结合 Kibana 与路由配置定位。
4. **关联完整性**：`global_id` 须能在 `t_fundout_bankcard_order` 找到银行卡明细，并能通过 Fundout->CMF 链路对应到 `cmf.tt_inst_order`（INST_ORDER_NO 形如 `ZAND20326031611337631`）。
5. **标准查询**：
   ```sql
   SELECT global_id, status, product_code, created_time, unity_result_code
   FROM mhtfundout.t_fundout_order
   WHERE partner_id = '<partner_id>' ORDER BY global_id DESC LIMIT 5;
   ```
6. **VS 回调后回写**：VS 成功后 CMF 状态置 `S`，Fundout 主表 `status` 应同步置 `SUCCESS`；若 VS 已到但仍停留在 In Process，需检查 `router.t_channel_result_code` 映射（`result_status=S` for PROCESSED）。

---
id: tbl_router_t_channel_result_code
object_type: Table
domain: payment-tools
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:7f334321-3b49-4c87-b6d9-8949925a962a
tags:
- router
- mapping
- result-code
subdomain: channel-routing
module: router
sensitivity: normal
name: 渠道返回码映射表 t_channel_result_code
aliases: []
related_services:
- svc_router
---

## 用途
位于 `router` 库，用于将 ZAND 银行返回码映射到 CMF 内部状态。决定 SP/SQ/VS 回执经路由器解析后写入 `cmf.tt_inst_order` / `cmf.tt_inst_order_result` 的最终 `INST_STATUS`(I/S/F/U)。

## 关键列
| 列名 | 说明 |
|---|---|
| channel_code | 渠道编码(如 ZAND201、ZAND203、ZAND204、ZAND207、ZAND210) |
| api_type | 接口类型：SP / SQ / VS |
| result_code | 银行返回的主码 |
| result_sub_code | 银行返回的子码 |
| result_status | 映射到 CMF 的状态(S=Success, F=Failed, I=In Process, U=Unknown) |

## 主键/索引
原文未提供，未作记录。

## 校验点(QA 关注)
- 当 VS 回调到达但订单仍停留在 In Process(`INST_STATUS=I`)时，常见根因是 `router.t_channel_result_code` 映射错误。需确认 VS 对应的 `result_code/result_sub_code`(如 PROCESSED) 映射到 `result_status=S`。
- 域内 VS：`MEMO=Credited To Beneficiary`，Type=`OUTGOING_DOMESTIC_TRANSACTION_STATUS` 应映射为 S。
- 国际 VS：`MEMO=PROCESSED`，Type=`OUTGOING_INTERNATIONAL_TRANSACTION_STATUS` 应映射为 S。
- 不同 channel_code(ZAND201/203/204/207/210) 应分别配置 SP / SQ / VS 三类 api_type 的映射，避免漏配导致状态不更新。

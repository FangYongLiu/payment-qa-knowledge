---
id: tbl_cmf_tt_inst_order_result
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
- sp
- sq
- vs
subdomain: cmf-router
module: null
sensitivity: normal
name: CMF指令结果表 tt_inst_order_result
aliases:
- tt_inst_order_result
related_services: []
related_tables:
- tbl_cmf_tt_inst_order
- tbl_router_t_channel_result_code
- tbl_mhtfundout_t_fundout_order
related_scenarios:
- scn_zand_fundout_test_cases
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
位于 `cmf` 库，记录 CMF Router 与 ZAND 银行交互的每一次 API 执行结果，对应 SP(Submit Payment)、SQ(Status Query)、VS(Vendor Status webhook) 三类调用。每条 `tt_inst_order` 通常会对应多条结果行：
- 域内 (ZAND201/204/210)：SP -> VS 两行
- 跨境 (ZAND203/207)：SP -> SQ(可能多次) -> VS 多行

用于追踪资金出款指令在渠道侧的实际状态变化、ChannelRefId 来源、以及最终成功/失败的判定依据。

## 关键列
| 列 | 说明 |
| --- | --- |
| `INST_ORDER_NO` | 关联 `tt_inst_order.INST_ORDER_NO`，CMF 渠道单号 (ZAND+channel 开头) |
| `API_TYPE` | 取值 `SP` / `SQ` / `VS`，标识本行属于哪一类 API 调用 |
| `INST_STATUS` | 单次 API 后状态：`I`(In Process)、`S`(Success)、`F`(Failed)、`U`(Unknown) |
| `INST_SEQ_NO` | 渠道返回的 ChannelRefId：域内以 `D` 开头(如 `D773644227520987`)，跨境以 `ZIT` 开头(如 `ZIT3657863264122`) |
| `EXTENSION` | 扩展字段，含 `CreationDateTime` / `ChannelRefId` / `channelTransTime` 等；SP/SQ/VS 三行应保持一致 |
| `MEMO` | 渠道返回备注，VS 域内 = `Credited To Beneficiary`，VS 跨境 = `PROCESSED`；同时含 Type，如 `OUTGOING_DOMESTIC_TRANSACTION_STATUS` / `OUTGOING_INTERNATIONAL_TRANSACTION_STATUS` |
| `GMT_CREATE` | 该结果行写入时间，按 ASC 排序可还原 SP -> SQ -> VS 时序 |

## 主键/索引
原文未给出主键/索引定义。常用查询键为 `INST_ORDER_NO`，按 `GMT_CREATE ASC` 排序追溯调用链。

## 校验点(QA 关注)
- **SP 行**：`API_TYPE=SP`、`INST_STATUS=I`、`INST_SEQ_NO` 是 `D...` 或 `ZIT...`；`EXTENSION` 必须含 `CreationDateTime`、`ChannelRefId`、`channelTransTime`。
- **SQ 行(仅跨境)**：`API_TYPE=SQ`、`INST_STATUS=I` 或 `S`；`ChannelRefId` 与 SP 一致；`EXTENSION` 与 SP 一致。
- **VS 行 - 域内**：`API_TYPE=VS`、`INST_STATUS=S`、`MEMO=Credited To Beneficiary`、Type=`OUTGOING_DOMESTIC_TRANSACTION_STATUS`。
- **VS 行 - 跨境**：`API_TYPE=VS`、`INST_STATUS=S`、`MEMO=PROCESSED`、Type=`OUTGOING_INTERNATIONAL_TRANSACTION_STATUS`。
- **Extension 一致性**：SP/SQ/VS 三行的 `CreationDateTime`、`ChannelRefId`、`channelTransTime` 应严格一致(TC-010)。
- **VS 入库但订单仍为 In Process**：检查 `router.t_channel_result_code` 中对应映射，确认 `PROCESSED` 的 `result_status=S`。
- **Mock VS 校验**：通过 mock 工具(HMAC key `CoQnNYbgefTzpvhV1yr8L/Q7RX0m/JjsWMEFmQRFTj8=`，URL `https://uat-fcw.test2pay.com/fcw/zand/notify`) 触发后，必须能在本表看到 VS 行落地。
- **SQ 长时间无 VS**：若 `tt_inst_order.RETRY_TIMES > 50` 仍无 VS 行写入，需 Mock VS 或联系 ZAND 团队；`RETRY_TIMES=54` 后停止轮询，SQ 行不再增加。
- 标准排查 SQL：
  ```sql
  SELECT INST_ORDER_NO, API_TYPE, INST_STATUS, MEMO, INST_SEQ_NO, EXTENSION, GMT_CREATE
  FROM cmf.tt_inst_order_result
  WHERE INST_ORDER_NO = '<order>' ORDER BY GMT_CREATE ASC;
  ```

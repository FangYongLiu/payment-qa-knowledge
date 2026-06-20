---
id: tbl_cmf_tt_inst_order_result
object_type: Table
domain: fund-out-transfer
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:AQ/2049867832
tags:
- cmf
- sp-sq-vs
- zand
subdomain: cmf
module: null
sensitivity: normal
name: CMF SP/SQ/VS结果表 tt_inst_order_result
aliases:
- tt_inst_order_result
related_services: []
related_tables:
- tbl_cmf_tt_inst_order
- tbl_mhtfundout_t_fundout_order
- tbl_mhtfundout_t_fundout_bankcard_order
related_scenarios:
- scn_zand_fundout_test_cases
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
位于 `cmf` 库，记录 CMF 与 ZAND 银行交互的每一次 API 调用结果，包括 SP(Submit Payment)、SQ(Status Query)、VS(Vendor Status webhook 回调)三类。每个 `INST_ORDER_NO` 对应多条结果记录，按调用先后写入；用于追溯订单生命周期、校验扩展字段一致性以及定位 VS 回调是否到达。

## 关键列
- `INST_ORDER_NO`：CMF 渠道订单号，关联 `tt_inst_order`(如 `ZAND20326031611337631`)
- `API_TYPE`：调用类型，取值 `SP` / `SQ` / `VS`
- `INST_STATUS`：该次调用的状态
  - SP：`I`(In Process)
  - SQ：`I` 或 `S`
  - VS：`S`(Success)
- `INST_SEQ_NO`：银行返回的 ChannelRefId
  - 国内：以 `D` 开头，如 `D773644227520987`
  - 国际：以 `ZIT` 开头，如 `ZIT3657863264122`
- `EXTENSION`：扩展字段，包含 `CreationDateTime`、`ChannelRefId`、`channelTransTime` 等
- `MEMO`：备注/银行返回信息
  - VS 国内：`Credited To Beneficiary`，Type=`OUTGOING_DOMESTIC_TRANSACTION_STATUS`
  - VS 国际：`PROCESSED`，Type=`OUTGOING_INTERNATIONAL_TRANSACTION_STATUS`
- `GMT_CREATE`：记录创建时间，用于按调用顺序排序

## 主键/索引
原文未明确给出主键/索引定义。按使用模式：以 `INST_ORDER_NO` 为查询入口，配合 `API_TYPE` 与 `GMT_CREATE` 排序检索。

典型查询：
```sql
SELECT INST_ORDER_NO, API_TYPE, INST_STATUS, MEMO, INST_SEQ_NO, EXTENSION, GMT_CREATE
FROM cmf.tt_inst_order_result
WHERE INST_ORDER_NO = '<order>' ORDER BY GMT_CREATE ASC;
```

## 校验点(QA 关注)
- **SP 行**：`INST_STATUS=I`；`INST_SEQ_NO` 为 `D...`(国内) 或 `ZIT...`(国际)；`EXTENSION` 必须含 `CreationDateTime`、`ChannelRefId`、`channelTransTime`
- **SQ 行(仅国际 ZAND203/207)**：`INST_STATUS=I` 或 `S`；`ChannelRefId` 与 SP 一致；`EXTENSION` 与 SP 保持一致
- **VS 行(国内)**：`INST_STATUS=S`；`MEMO=Credited To Beneficiary`；Type=`OUTGOING_DOMESTIC_TRANSACTION_STATUS`
- **VS 行(国际)**：`INST_STATUS=S`；`MEMO=PROCESSED`；Type=`OUTGOING_INTERNATIONAL_TRANSACTION_STATUS`
- **国内流程**：应只有 SP + VS 两条记录(无 SQ)，~12 秒内完成
- **国际流程**：应有 SP + 多条 SQ + 最终 VS；若 SQ 累计达到 `RETRY_TIMES=54` 仍无 VS，需通过 Mock VS 工具补发或联系 ZAND
- **扩展字段一致性**：SP/SQ/VS 三类记录的 `CreationDateTime`、`ChannelRefId`、`channelTransTime` 必须一致(TC-010 重点)
- **VS 未到达排查**：检查 FCW Webhook(HMAC 校验)；UAT HMAC key 为 `CoQnNYbgefTzpvhV1yr8L/Q7RX0m/JjsWMEFmQRFTj8=`；回调 URL `https://uat-fcw.test2pay.com/fcw/zand/notify`
- **VS 已到但订单仍 In Process**：检查 `router.t_channel_result_code` 映射，`PROCESSED` 应映射为 `result_status=S`

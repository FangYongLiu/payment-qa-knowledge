---
title: ZAND Fundout常见问题排查
domain: fund-out-transfer
kind: wiki_page
slug: zand-fundout-troubleshooting
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:7f334321-3b49-4c87-b6d9-8949925a962a
tags: []
---

# ZAND Fundout常见问题排查

本页汇总 ZAND Fundout 在 UAT 环境常见的故障现象、根因与处置方法，便于 QA 在订单异常时快速定位。完整流程见 [[zand-fundout-overview]]，链路与表结构见 [[zand-fundout-system-architecture]]。

## 故障速查表

| 现象 | 可能原因 | 处置 |
|---|---|---|
| 订单已创建但 CMF 中查不到 | `unity_result_code = cmf.route.fail`（路由失败） | 查 Kibana 日志与路由配置 |
| SP 已受理但 VS 一直不到 | SQ `RETRY_TIMES > 50`，已接近停止轮询 | 发送 Mock VS、找 Zand 团队确认，或重置 RETRY_TIMES |
| VS 已收到但订单仍停留 In Process | `router.t_channel_result_code` 映射错误 | 确认 `PROCESSED` 对应的 `result_status=S` |
| VS 报 `Invalid signature` | HMAC 密钥错误 | 使用对应环境（UAT/SIM）正确密钥 |
| 银行拒绝：`BIC and destination country mismatch` | 受益人 `countryCode` 与 BIC 国家不一致 | 重新创建受益人并填写正确国家 |
| 路由到 `TEST201` 而不是 `ZAND203` | 商户路由配置错误 | 更新 CMF 中的 partner routing |

## 路由失败：订单不进 CMF

- 现象：[[tbl_mhtfundout_t_fundout_order]] 中已生成订单，但 [[tbl_cmf_tt_inst_order]] 中无对应记录。
- 关键字段：`t_fundout_order.unity_result_code = cmf.route.fail`。
- 排查：
  - 查 Kibana 日志中 Fundout Service -> Kafka -> CMF Router 的路由信息。
  - 校验该 partner 的渠道路由是否正确（例如本应走 ZAND203 却落到 TEST201，需更新 CMF 的 partner routing）。

## SP 已发出但 VS 不到达

- 仅国际单（ZAND203 / ZAND207）依赖 SQ 轮询 + VS；域内单（ZAND201 / ZAND210）走 SP -> VS。
- 检查 [[tbl_cmf_tt_inst_order]] 的 `RETRY_TIMES`：
  - 超过 35 后轮询间隔会拉长到小时级。
  - 达到 54 即停止 SQ 轮询。
- 处置方式：
  - 使用 [[auto_zand_mock_vs_tool]] 手动回调 VS 完成订单。
  - 联系 ZAND 银行侧确认 ChannelRefId 状态。
  - 必要时重置 `RETRY_TIMES`，让 SQ 继续轮询。

## VS 已到但订单仍 In Process

- [[tbl_cmf_tt_inst_order_result]] 中存在 `API_TYPE=VS` 的记录，但 [[tbl_cmf_tt_inst_order]] `STATUS` 仍为 `I`。
- 根因通常在 [[tbl_router_t_channel_result_code]]：渠道返回码到 CMF 状态的映射缺失或错误。
- 检查项：
  - 国际单 VS 的 `MEMO=PROCESSED` 应映射到 `result_status=S`。
  - 域内单 VS 的 `MEMO=Credited To Beneficiary` 同理。
- 修正映射后该订单应被推进到 `S`，并由 DPM 完成扣款/手续费记账。

## VS 签名错误（Invalid signature）

- 现象：FCW Webhook 接收 VS 时校验 HMAC 失败。
- 根因：使用了错误环境的 HMAC Key。
- UAT 环境密钥：`CoQnNYbgefTzpvhV1yr8L/Q7RX0m/JjsWMEFmQRFTj8=`
- 回调地址：`https://uat-fcw.test2pay.com/fcw/zand/notify`
- 使用 Mock VS 工具时务必匹配环境，详见 [[auto_zand_mock_vs_tool]]。

## BIC 与国家不匹配（银行拒付）

- 现象：ZAND 银行返回 `BIC and destination country mismatch`，SP 直接被拒。
- 根因：受益人录入时 `countryCode` 与该 BIC 实际所属国家不一致。
- 处置：删除/重建受益人，填入与 BIC 一致的国家代码，然后重新发起 Fundout。

## 路由错走到 TEST201

- 现象：本应走 ZAND203（国际 SWIFT）的订单，CMF 中 `FUND_CHANNEL_CODE=TEST201`。
- 根因：商户在 CMF 中的渠道路由未正确指向 ZAND 渠道。
- 处置：更新 partner routing 配置，确认相应 `product_code`（如 220402）映射到正确的 ZAND 渠道。

## 关联资源

- 排障所需 SQL 与字段含义：[[zand-fundout-test-guide]]
- 端到端流程参考：[[flow_zand_fundout]]
- 用例覆盖：[[scn_zand_fundout_test_cases]]

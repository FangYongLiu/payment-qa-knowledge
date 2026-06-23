---
title: ZAND Fundout常见问题排查
domain: fund-out-transfer
kind: wiki_page
slug: zand-fundout-troubleshooting
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2049867832
tags: []
---

# ZAND Fundout常见问题排查

本页汇总 ZAND Fundout 在 UAT 测试与生产排障中常见的故障症状、根因与处理方式，覆盖路由、SP/SQ/VS 各阶段以及回调签名等关键环节。相关测试方法见 [[zand-fundout-testing-guide]]，系统调用链见 [[zand-fundout-system-architecture]]。

## 常见症状与解决方案

| 症状 | 可能原因 | 处理方式 |
|---|---|---|
| 订单已创建但 CMF 中无对应记录 | `unity_result_code = cmf.route.fail` | 查 Kibana 日志，检查路由配置 |
| SP 已受理但始终未收到 VS | SQ `RETRY_TIMES > 50` | 发送 Mock VS、联系 Zand 团队，或重置 retries |
| 收到 VS 但订单仍处于 In Process | `router.t_channel_result_code` 映射错误 | 确认 PROCESSED 对应 `result_status=S` |
| VS 提示 Invalid signature | HMAC key 错误 | 按环境(UAT/SIM)使用正确的 key |
| Bank 拒绝：`BIC and destination country mismatch` | Beneficiary `countryCode` 不一致 | 用正确的 country 重新创建 beneficiary |
| 路由到 TEST201 而非 ZAND203 | Partner 路由配置错误 | 在 CMF 配置中更新 partner 路由 |

## 路由与下单阶段

- **症状**：Fundout 订单已落库，但 [[tbl_cmf_tt_inst_order]] 中查不到对应 `INST_ORDER_NO`。
- **判定**：检查 [[tbl_mhtfundout_t_fundout_order]] 的 `unity_result_code`，若为 `cmf.route.fail` 即路由失败。
- **处理**：
  - 查 Kibana 日志定位 CMF Router 异常。
  - 核对 partner 路由配置，确认目标渠道(ZAND201/203/204/207/210)。
  - 若错误地路由到 `TEST201`，需更新 CMF partner 路由配置。

## SP 阶段问题

- **SP 失败/超时**：由 retry handler 以指数退避方式入重试队列，由 worker 重新提交；若达到永久失败则反向冲销手续费。
- **银行拒单**：常见 `BIC and destination country mismatch`，根因是 beneficiary 的 `countryCode` 与 BIC 国家不一致；需重建 beneficiary。

## SQ 轮询问题

- 前 ~2 分钟密集轮询，间隔逐步增大；`RETRY_TIMES > 35` 后间隔达到小时级；`RETRY_TIMES = 54` 时停止。
- **症状**：SP 已成功(返回 `ZIT...`)但久未推进。
- **处理**：
  - 若 `RETRY_TIMES > 50`，可使用 Mock VS 工具补推回调（参见 [[auto_zand_mock_vs_tool]]）。
  - 必要时联系 Zand 团队确认银行侧最终状态，或重置 retries 重新轮询。

## VS 回调问题

### Invalid signature
- 原因：HMAC 密钥与环境不匹配。
- 处理：按环境取正确 key；UAT 使用 `CoQnNYbgefTzpvhV1yr8L/Q7RX0m/JjsWMEFmQRFTj8=`，回调地址 `https://uat-fcw.test2pay.com/fcw/zand/notify`。

### VS 已收到但订单未流转到 SUCCESS
- 原因：`router.t_channel_result_code` 中渠道结果到 CMF 状态的映射缺失或错误。
- 处理：确认对应 `channel_code` + `api_type=VS` 下的 result code（如国际 `PROCESSED`、国内 `Credited To Beneficiary`）映射为 `result_status=S`。
- 验证：查询 [[tbl_cmf_tt_inst_order_result]]，确认存在 `API_TYPE=VS` 且 `INST_STATUS=S` 的行。

## Extension 字段一致性

- SP/SQ/VS 三阶段的 `EXTENSION` 应保持 `CreationDateTime`、`ChannelRefId`、`channelTransTime` 一致。
- 不一致通常意味着串单或回调匹配错误，应以 `INST_SEQ_NO`(`D.../ZIT...`) 为关键字横向比对。

## 排查常用 SQL

按 `partner_id` / `INST_ORDER_NO` 关联查询：

- `mhtfundout.t_fundout_order` 看主单 `status`、`unity_result_code`。
- `cmf.tt_inst_order` 看渠道单 `STATUS`、`RETRY_TIMES`。
- `cmf.tt_inst_order_result` 按 `GMT_CREATE` 升序查看 SP -> SQ -> VS 轨迹。

具体语句见 [[zand-fundout-testing-guide]]。

## 相关链接

- 业务与渠道总览：[[zand-fundout-overview]]
- 端到端流程：[[flow_zand_fundout]]
- 核心用例：[[scn_zand_fundout_test_cases]]
- Mock VS 工具：[[auto_zand_mock_vs_tool]]

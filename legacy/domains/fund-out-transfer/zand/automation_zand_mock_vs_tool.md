---
id: auto_zand_mock_vs_tool
object_type: AutomationAsset
domain: fund-out-transfer
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:AQ/2049867832
tags:
- mock
- VS
- HMAC
- UAT
subdomain: zand
module: testing
sensitivity: normal
name: ZAND Mock VS回调工具
aliases:
- Zand.java
- Mock VS Callback Tool
related_services: []
related_tables:
- tbl_cmf_tt_inst_order
- tbl_cmf_tt_inst_order_result
related_scenarios:
- scn_zand_fundout_test_cases
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
用于国际订单(ZAND203/ZAND207)在测试环境中无法等待真实VS回调时，手动构造并发送VS Vendor Status Webhook 回调到 FCW，使订单从 In Process(I) 推进到 Success(S)，完成端到端测试闭环。

适用场景：
- 国际SWIFT转账(ZAND203)：SP已成功，需要VS回调以将 `cmf.tt_inst_order_result` 中 INST_STATUS 从 I 更新为 S，MEMO=PROCESSED。
- 结算国际转账(ZAND207)：同上，需要VS触发最终状态。
- TC-008 Mock VS callback validation 测试用例。

## 使用方式
1. 从数据库拿到目标订单的关键参数：
   - ChannelRefId(国际订单以 `ZIT` 开头)：来自 `cmf.tt_inst_order_result` SP 行的 `INST_SEQ_NO` 或 EXTENSION。
   - CMF 订单号(`INST_ORDER_NO`，以 `ZAND` 开头)：来自 `cmf.tt_inst_order`。
   - 订单金额。
2. 编辑代码仓库 `cgs-apitest` 中的 `Zand.java` mock 工具，填入正确的：
   - amount(金额)
   - channel_ref(ChannelRefId, ZIT...)
   - instruction_id
3. 编译并运行 Zand.java，向目标URL发起带HMAC签名的VS回调请求。
4. 验证 `cmf.tt_inst_order_result` 中是否新增一条 API_TYPE=VS、INST_STATUS=S、MEMO=PROCESSED、Type=OUTGOING_INTERNATIONAL_TRANSACTION_STATUS 的记录。

## 关键配置
- HMAC Key (UAT)：`CoQnNYbgefTzpvhV1yr8L/Q7RX0m/JjsWMEFmQRFTj8=`
- 目标URL：`https://uat-fcw.test2pay.com/fcw/zand/notify`
- 代码位置：`cgs-apitest` Git 仓库中的 `Zand.java`
- 必填业务参数：amount、channel_ref(ZIT...)、instruction_id

## 注意事项
- HMAC Key 区分环境：UAT 与 SIM 使用不同 Key，错用会导致 FCW 返回 `Invalid signature`。
- ChannelRefId 必须与SP阶段返回的一致(国际订单以 ZIT 开头)，否则 FCW 无法关联到对应 CMF 订单。
- Extension 字段(CreationDateTime、ChannelRefId、channelTransTime)需与 SP/SQ 阶段保持一致，避免触发一致性校验失败。
- 仅适用于需要VS的国际订单(ZAND203/ZAND207)；域内订单(ZAND201/ZAND204/ZAND210)走 SP -> VS 快速链路，一般无需 mock。
- 若 VS 已收到但订单仍停留在 In Process，需检查 `router.t_channel_result_code` 中 PROCESSED -> result_status=S 的映射是否正确，而非重复发送 mock VS。
- 若 SQ RETRY_TIMES > 50 仍无VS，可使用本工具补发，或联系 Zand team / 重置 retries。
- 必须连接公司 VPN 才能访问 UAT FCW 域名。

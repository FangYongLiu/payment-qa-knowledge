---
id: auto_zand_mock_vs_tool
object_type: AutomationAsset
domain: fund-out-transfer
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:7f334321-3b49-4c87-b6d9-8949925a962a
tags:
- mock
- vs-callback
- hmac
- international
subdomain: null
module: null
sensitivity: normal
name: ZAND Mock VS回调工具
aliases: []
related_services:
- FCW Webhook Receiver
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
为国际单（ZAND203 / ZAND207）测试场景提供闭环手段：当真实 VS 回调未及时到达，或需要构造特定 VS 状态时，由测试人员通过 Zand.java mock 工具构造带 HMAC 签名的 VS 报文，主动调用 FCW 的 ZAND 回调接收端点，将 CMF 订单从 `INST_STATUS=I` 推进到 `S`，完成 SP -> SQ -> VS 完整链路验证。

适用场景：
- TC-008 Mock VS callback validation
- 国际 SWIFT 转账（ZAND203）测试用例 TC-002 中等待 VS 阶段
- 国际单 SQ 轮询超过阈值（RETRY_TIMES > 50）但 VS 一直不到达的排障
- Settlement international（ZAND207）需要补 VS 才能将订单置为 SUCCESS 时

## 使用方式
针对国际订单（需要 VS 才能完结）：
1. 从 DB 查询拿到 ChannelRefId（以 `ZIT` 开头）以及对应的 CMF 订单号（INST_ORDER_NO）。
2. 编辑 cgs-apitest 仓库中的 `Zand.java` mock 工具，填入正确的：
   - amount（与订单金额一致）
   - channel_ref（即 ZAND 返回的 ChannelRefId，ZIT...）
   - instruction_id
3. 使用 UAT 环境 HMAC key：`CoQnNYbgefTzpvhV1yr8L/Q7RX0m/JjsWMEFmQRFTj8=`
4. Target URL（UAT）：`https://uat-fcw.test2pay.com/fcw/zand/notify`
5. 编译并运行 Zand.java，FCW 接收 VS 后会校验 HMAC 并回写 CMF。
6. 验证 `cmf.tt_inst_order_result` 中新增一条 `API_TYPE=VS` 记录，且 `INST_STATUS=S`、`MEMO=PROCESSED`、Type=OUTGOING_INTERNATIONAL_TRANSACTION_STATUS。

典型调用上下文：
- TC-002 步骤 "Then wait for real VS or send Mock VS"
- Troubleshooting: "SP accepted but VS never arrives" → Send Mock VS

## 关键配置
| 配置项 | 值 / 来源 |
|---|---|
| 工具源码 | cgs-apitest 仓库中的 `Zand.java` |
| HMAC Key (UAT) | `CoQnNYbgefTzpvhV1yr8L/Q7RX0m/JjsWMEFmQRFTj8=` |
| 目标 URL (UAT) | `https://uat-fcw.test2pay.com/fcw/zand/notify` |
| 必填字段 | amount、channel_ref（ZIT...）、instruction_id |
| 接收端 | FCW Webhook Receiver（HMAC verify, update CMF） |

## 注意事项
- HMAC key 必须按环境匹配（UAT / SIM 各自不同）。若签名错误，VS 会被拒收并出现 `Invalid signature` 报错（见 Troubleshooting）。
- channel_ref 必须使用 ZAND 返回的真实 ChannelRefId（国际单以 `ZIT` 开头），否则 FCW 无法关联到 CMF 订单。
- 该工具仅用于国际单（ZAND203 / ZAND207）补发 VS；国内单（ZAND201/204/210）SP -> VS 在约 12 秒内自动完成，通常不需要 mock。
- 若 VS 已到达但订单仍停留 In Process，问题不在 mock 工具，而在 `router.t_channel_result_code` 的映射（需确保 `PROCESSED` 对应 `result_status=S`）。
- 运行 mock 后必须通过校验 SQL 查询 `cmf.tt_inst_order_result` 确认 VS 行已写入，并核对 EXTENSION 中 CreationDateTime、ChannelRefId、channelTransTime 与 SP/SQ 一致。
- 该工具属于运行 cgs-apitest 测试框架的一部分，需先 VPN 接入并具备 cgs-apitest 仓库访问权限。

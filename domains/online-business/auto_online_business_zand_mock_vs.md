---
id: auto_online_business_zand_mock_vs
object_type: AutomationAsset
name: ZAND Mock VS 回调工具(Zand.java)
aliases: [Zand.java, Mock VS Callback Tool, zand_mock_vs_tool]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: wiki:7f334321-3b49-4c87-b6d9-8949925a962a
tags: [online-business, fundout, zand, mock, vs-callback, hmac]
related_scenarios: [scn_online_business_zand_fundout]
related_services: [svc_fcw, svc_cmf]
---

# ZAND Mock VS 回调工具(Zand.java)

> 来源 cgs-apitest 仓库 `Zand.java`。覆盖场景 [[scn_online_business_zand_fundout]](TC-008)。

## 用途
为国际单(ZAND203 / ZAND207)测试提供闭环手段:当真实 VS 回调未及时到达,或需构造特定 VS 状态时,由测试人员通过 `Zand.java` 构造带 HMAC 签名的 VS 报文,主动调用 [[svc_fcw]] 的 ZAND 回调端点,将 CMF 订单从 `INST_STATUS=I` 推进到 `S`,完成 SP→SQ→VS 完整链路验证。

适用场景:
- TC-008 Mock VS callback validation
- 国际 SWIFT 转账(ZAND203)TC-002 等待 VS 阶段
- 国际单 SQ 轮询超阈值(`RETRY_TIMES > 50`)但 VS 一直不到达的排障(见 [[ts_zand_fundout]])
- Settlement international(ZAND207)需补 VS 才能置 SUCCESS 时

## 关联关系
- **覆盖的场景**:[[scn_online_business_zand_fundout]]
- **针对/跑在的服务**:[[svc_fcw]](接收 VS 回调并回写 CMF)、[[svc_cmf]]
- **相关流程/排障**:[[flow_zand_fundout]]、[[ts_zand_fundout]]

## 使用方式
针对国际订单(需 VS 才能完结):
1. 从 DB 取 ChannelRefId(以 `ZIT` 开头,来自 `cmf.tt_inst_order_result` SP 行的 `INST_SEQ_NO` 或 EXTENSION)与对应 CMF 订单号(`INST_ORDER_NO`,以 `ZAND` 开头)。
2. 编辑 cgs-apitest 仓库的 `Zand.java`,填入正确的:`amount`(与订单金额一致)、`channel_ref`(ZAND 返回的 ChannelRefId,`ZIT...`)、`instruction_id`。
3. 使用 UAT 环境 HMAC key:`CoQnNYbgefTzpvhV1yr8L/Q7RX0m/JjsWMEFmQRFTj8=`。
4. Target URL(UAT):`https://uat-fcw.test2pay.com/fcw/zand/notify`。
5. 编译运行 `Zand.java`,FCW 校验 HMAC 后回写 CMF。
6. 验证 `cmf.tt_inst_order_result` 新增一条 `API_TYPE=VS` 记录,且 `INST_STATUS=S`、`MEMO=PROCESSED`、Type=`OUTGOING_INTERNATIONAL_TRANSACTION_STATUS`。

## 关键配置
| 配置项 | 值 / 来源 |
|---|---|
| 工具源码 | cgs-apitest 仓库 `Zand.java` |
| HMAC Key (UAT) | `CoQnNYbgefTzpvhV1yr8L/Q7RX0m/JjsWMEFmQRFTj8=` |
| 目标 URL (UAT) | `https://uat-fcw.test2pay.com/fcw/zand/notify` |
| 必填字段 | amount、channel_ref(`ZIT...`)、instruction_id |
| 接收端 | FCW Webhook Receiver(HMAC verify,update CMF) |

## 注意事项
- HMAC key 必须按环境匹配(UAT / SIM 各自不同);错用会触发 `Invalid signature`。
- channel_ref 必须用 ZAND 返回的真实 ChannelRefId(国际单 `ZIT` 开头),否则 FCW 无法关联到 CMF 订单。
- 仅用于国际单(ZAND203/207);境内单(ZAND201/204/210)SP→VS 约 12s 自动完成,通常无需 mock。
- 若 VS 已到但订单仍 In Process,问题在 `router.t_channel_result_code` 映射(确保 `PROCESSED` 对应 `result_status=S`),而非重复发 mock。
- 运行后必须校验 `cmf.tt_inst_order_result` 确认 VS 行写入,并核对 EXTENSION 中 CreationDateTime、ChannelRefId、channelTransTime 与 SP/SQ 一致。
- 需先 VPN 接入并具备 cgs-apitest 仓库访问权限。

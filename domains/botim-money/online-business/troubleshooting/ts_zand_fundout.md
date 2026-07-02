---
id: ts_zand_fundout
object_type: Troubleshooting
name: ZAND渠道出款常见故障排查
aliases: [ZAND Fundout Troubleshooting]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/2049867832
tags: [online-business, fundout, zand, 排障]
related_services: [svc_fundout, svc_cmf, svc_fcw]
related_tables: [tbl_mhtfundout_t_fundout_order, tbl_cmf_tt_inst_order, tbl_cmf_tt_inst_order_result, tbl_router_t_channel_result_code]
related_logs: []
related_failures: []
---

# ZAND渠道出款常见故障排查

## 症状
ZAND Fundout 在 UAT 测试与生产中常见的出款卡单/失败现象,集中在路由、SP/SQ/VS 各阶段以及 VS 回调签名环节。

## 关联关系
- **涉及服务 / 表**:[[svc_fundout]] / [[svc_cmf]] / [[svc_fcw]];[[tbl_mhtfundout_t_fundout_order]]、[[tbl_cmf_tt_inst_order]]、[[tbl_cmf_tt_inst_order_result]]、[[tbl_router_t_channel_result_code]](= `related_services` / `related_tables`)
- **相关流程 / 场景**:[[flow_zand_fundout]]、[[scn_online_business_zand_fundout]];补发 VS 工具 [[auto_online_business_zand_mock_vs]]

## 常见症状与处理
| 症状 | 可能根因 | 处理方式 |
|---|---|---|
| 订单已创建但 CMF 中无对应记录 | `unity_result_code = cmf.route.fail` | 查 Kibana 日志,核对路由配置 |
| SP 已受理但始终未收到 VS | SQ `RETRY_TIMES > 50` | 发 Mock VS、联系 Zand 团队,或重置 retries |
| 收到 VS 但订单仍 In Process | `router.t_channel_result_code` 映射错误 | 确认 PROCESSED 对应 `result_status=S` |
| VS 提示 Invalid signature | HMAC key 错误 | 按环境(UAT/SIM)使用正确 key |
| Bank 拒绝 `BIC and destination country mismatch` | Beneficiary `countryCode` 与 BIC 国家不一致 | 用正确 country 重建 beneficiary |
| 路由到 TEST201 而非 ZAND203 | Partner 路由配置错误 | 在 CMF 配置中更新 partner 路由 |

## 可能根因(分阶段)
### 路由与下单阶段
- 现象:Fundout 订单已落库,但 [[tbl_cmf_tt_inst_order]] 查不到对应 `INST_ORDER_NO`。
- 判定:检查 [[tbl_mhtfundout_t_fundout_order]] 的 `unity_result_code`,若为 `cmf.route.fail` 即路由失败。
- 处理:查 Kibana 定位 CMF Router 异常;核对 partner 路由配置确认目标渠道;若误路由到 `TEST201` 需更新 CMF partner 路由。

### SP 阶段
- SP 失败/超时:由 retry handler 以指数退避入重试队列,worker 重提;永久失败则反向冲销手续费。
- 银行拒单:常见 `BIC and destination country mismatch`,根因是 beneficiary `countryCode` 与 BIC 国家不一致,需重建 beneficiary。

### SQ 轮询阶段
- 前 ~2 分钟密集轮询,间隔逐步增大;`RETRY_TIMES>35` 后小时级;`RETRY_TIMES=54` 停止。
- 现象:SP 已成功(返回 `ZIT...`)但久未推进。
- 处理:`RETRY_TIMES>50` 可用 Mock VS 补推(见 [[auto_online_business_zand_mock_vs]]);必要时联系 Zand 团队或重置 retries。

### VS 回调阶段
- **Invalid signature**:HMAC 密钥与环境不匹配。UAT 使用 `CoQnNYbgefTzpvhV1yr8L/Q7RX0m/JjsWMEFmQRFTj8=`,回调地址 `https://uat-fcw.test2pay.com/fcw/zand/notify`。
- **VS 已收到但未流转到 SUCCESS**:`router.t_channel_result_code` 中渠道结果→CMF 状态映射缺失/错误。确认对应 `channel_code` + `api_type=VS` 的 result code(国际 `PROCESSED`、境内 `Credited To Beneficiary`)映射为 `result_status=S`;查 [[tbl_cmf_tt_inst_order_result]] 确认存在 `API_TYPE=VS` 且 `INST_STATUS=S` 的行。

## 排查步骤
- DB:`mhtfundout.t_fundout_order` 看主单 `status`、`unity_result_code`;`cmf.tt_inst_order` 看渠道单 `STATUS`、`RETRY_TIMES`;`cmf.tt_inst_order_result` 按 `GMT_CREATE` 升序查看 SP → SQ → VS 轨迹。
- EXTENSION 一致性:SP/SQ/VS 三阶段 `EXTENSION` 的 CreationDateTime、ChannelRefId、channelTransTime 应一致;不一致以 `INST_SEQ_NO`(`D.../ZIT...`)为关键字横向比对,定位串单/回调错配。
- Kibana:按 `partner_id` / `INST_ORDER_NO` 关联检索 CMF Router 与 FCW 日志。

## 处理 / 规避
- 路由错配 → 修 CMF partner 路由配置后重试。
- 国际单久挂 → Mock VS 补发(确认 channel_ref 用真实 `ZIT...` ChannelRefId)。
- 映射缺失 → 补全 `router.t_channel_result_code` 的 result_status 映射,不要重复发 mock。

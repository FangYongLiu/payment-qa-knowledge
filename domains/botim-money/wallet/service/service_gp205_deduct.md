---
id: svc_deduct
object_type: Service
domain: wallet
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp205
name: deduct
dev_owner: Guoyou.Ma
aliases: [gp205_deduct]
related_services: [svc_member, svc_protocol, svc_tradeii, svc_acs, svc_voucher, svc_pns, svc_cashdesk_api, svc_grc_check_identity_provider, svc_authpay, svc_mns_main, svc_cmf]
related_tables: []
related_scenarios: [scn_online_business_auto_debit]
---

# deduct

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp205` · domain=`wallet`。

## 作用
自动代扣执行（queryProtocol，调 protocol/trade）

## 系统中的位置
- 功能层:会员 / 账户 / 卡 / 协议 (Member / Account / Card)
- 业务域:`wallet`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_member]] member（会员 / 账户核心） · 21450 次 · high
- [[svc_protocol]] protocol（代扣 / 签约协议管理） · 9607 次 · high
- [[svc_tradeii]] tradeii（交易订单引擎） · 2086 次 · high
- [[svc_acs]] acs（反欺诈 / 风控 + 渠道密钥） · 995 次 · high
- [[svc_voucher]] voucher（全局 ID 与幂等凭证） · 818 次 · high
- [[svc_pns]] pns（支付通知服务） · 675 次 · high
- [[svc_cashdesk_api]] cashdesk-api（统一收银台） · 654 次 · high
- [[svc_grc_check_identity_provider]] grc-check-identity-provider（风控合规身份校验） · 272 次 · med·待核实
- [[svc_authpay]] authpay（授权支付 / 免密代扣执行） · 225 次 · high
- [[svc_mns_main]] mns-main（消息通知中枢） · 140 次 · med·待核实
- [[svc_cmf]] cmf（渠道管理与资金） · 79 次 · high

**被调用(上游)—— 这些服务调用本服务:**
tradeii

## 参与的业务场景(cgs 回归)
- §3. 自动代扣 / 签约（`test_auto_debit`）

## 关键方法 / 入口(UAT 实测)
- `queryProtocol`(查代扣协议);执行 AUTODEBIT:凭 `authProtocolNo`(= `t_deduct_protocol.deduct_protocol_no`)→ [[svc_authpay]] 鉴权 → [[svc_tradeii]] 扣款 → [[svc_pns]] 通知。

## 涉及的 API / 数据库表
- **暴露 API**(Dubbo,来源 `deduct-dubbo-api` 文档):`PayOrderFacade.protocolPay`(凭协议号代扣)、`DeductProtocolFacade.protocolApply`(发起签约申请,支持交易完成后延迟签约)、`DeductProtocolQueryFacade.queryProtocol`(查协议状态/签约人)。协议管理下沉 [[svc_protocol]]。
- **读写的表**:[[tbl_deduct_t_deduct_protocol]](可用代扣协议 `status=A`)、[[tbl_deduct_t_deduct_protocol_apply]](签约申请 `status=S`)、[[tbl_deduct_t_deduct_protocol_config]](扣款服务配置 `protocol_scene_code` 120/111)。

## 测试要点 / 排障 / 常见问题(UAT 实测)
- **代扣执行前提**:`authProtocolNo` 对应的 `t_deduct_protocol` 必须 `status=A`(已签约可用);否则代扣拒绝。
- **链路**:AUTODEBIT 下单 → deduct 查协议 → authpay 鉴权(商户组/方案/策略)→ tradeii 扣款 → 落交易 `trade_status=SS`。
- **怎么测/定位**:先跑签约(见 [[svc_protocol]] 签约数据链)拿 `deduct_protocol_no`,再用它作 `authProtocolNo` 下单;失败先查协议状态 A。
- 完整场景见 [[scn_online_business_auto_debit]]。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[auto_online_business_auto_debit]](自动化:自动代扣自动化)
- [[flow_cashier_payment]](流程:收银台 / 收单卡支付端到端流程（含退款）)
- [[scn_online_business_auto_debit]](场景:自动代扣 / 签约 (Auto Debit))

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp205` · domain=`wallet`。

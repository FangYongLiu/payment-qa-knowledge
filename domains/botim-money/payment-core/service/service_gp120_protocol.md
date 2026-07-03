---
id: svc_protocol
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp120
name: protocol
dev_owner: Gangling.Shen
aliases: [gp120_protocol]
related_services: []
related_tables: []
---

# protocol

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp120` · domain=`payment-core`。

## 作用
代扣 / 签约协议管理（被 cashdesk/cashier/deduct 调用）

## 系统中的位置
- 功能层:会员 / 账户 / 卡 / 协议 (Member / Account / Card)
- 业务域:`payment-core`

## 关联关系

**被调用(上游)—— 这些服务调用本服务:**
cashdesk-api, cashierii, deduct

## 涉及的 API / 数据库表
**暴露 / 相关 API:** [[api_payby_get_protocol]] 查询协议接口、[[api_payby_apply_protocol]] 申请签约协议接口、[[api_payby_protocol_notify]] 签约协议结果通知接口
**读写的表:** [[tbl_protocol_t_contract_sign_info]] 签约协议信息表 t_contract_sign_info、[[tbl_deduct_t_deduct_protocol]] 代扣协议表 t_deduct_protocol

## 参与的业务场景(cgs 回归)
- §2. 收银台 / 收银（`test_bpg_paypage` 收银侧、cashier 用例）
- §3. 自动代扣 / 签约（`test_auto_debit`）

## 关键方法 / 入口(UAT 实测)
- `querySimpleApply`(查签约模板,返回 `templateNo=02001`、`applyVoucherNo`、`signerId`、`merchantId`、`partnerId`)、`apply`(申请签约)、`notify`(签约结果通知)。经 [[svc_cashdesk_api]]/[[svc_cashierii]] 收银台发起,或 PAYANDSIGN。

## 签约数据链(UAT 实测)
1. **申请**:querySimpleApply/apply → 生成签约申请([[tbl_deduct_t_deduct_protocol_apply]] `status=S`)。
2. **用户确认**:用户登录 App 确认签约。
3. **生效**:成功后 [[tbl_protocol_t_contract_sign_info]] `status=EFFECTIVE`(`sign_contract_no`,如 2520250424…)+ [[tbl_deduct_t_deduct_protocol]] `status=A`(`deduct_protocol_no`)。
4. **代扣**:`deduct_protocol_no` 即 AUTODEBIT 下单的 `authProtocolNo`,由 [[svc_deduct]] 执行。
- 服务 ID:`protocol_scene_code`(PAYANDSIGN 的 `protocolSceneCode`)配置于 [[tbl_deduct_t_deduct_protocol_config]](常量 120 / SIM 111)。

## 测试要点 / 排障 / 常见问题
- **签约状态流转**:apply(S)→ 用户确认 → contract_sign_info(EFFECTIVE)+ deduct_protocol(A);任一未推进则代扣不可用。
- **怎么测/定位**:按 `sign_contract_no`/`deduct_protocol_no` 核对三表状态;代扣失败先查协议是否 EFFECTIVE/A。
- 完整签约→代扣场景见 [[scn_online_business_auto_debit]]。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[scn_botim_vip_auto_sign_protocol]](场景:Botim VIP 会员协议自动签署)
- [[ts_payby_auth_protocol_return_codes]](排障:PayBy 授权协议签约 / 转账接口返回码排错)

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp120` · domain=`payment-core`。

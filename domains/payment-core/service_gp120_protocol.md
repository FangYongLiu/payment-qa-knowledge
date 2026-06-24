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

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题

**UAT Kibana 7d 错误观测**(自动回归 + UAT 流量,app_id=`protocol`):
- ERROR 657 次,主要:`SignProtocolBySubTypeProcessor`×640
- WARN 261 次,主要:`SignProtocolByVoucherNoProcessor`×154、`ContractServiceImpl`×89
- ⚠️ 频次可能含 UAT 测试数据噪声,**真坑 vs 噪声需人工确认**;高频项见域级排障对象。
- 更多 QA 校验点(怎么测 / 已知坑 / 典型故障定位)待补。
## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp120` · domain=`payment-core`。

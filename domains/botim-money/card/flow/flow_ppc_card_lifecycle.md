---
id: flow_ppc_card_lifecycle
object_type: Flow
name: PPC 卡端到端业务流程(开卡→激活→交易→清算→关卡)
aliases: [PPC card lifecycle, 卡业务主流程]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/2134442046 + AQ/2133098640 (PPC 业务定义层 + API 清单)
tags: [ppc, card, lifecycle, flow]
related_services: [svc_ppc, svc_cgs]
related_tables: [tbl_ppc_t_virtual_card]
related_scenarios: [scn_card_lifecycle_transitions]
---

# PPC 卡端到端业务流程

## 概述
PPC 预付卡产品的端到端业务主流程:开卡 → 激活 → 消费授权 → 清算入账 → 退款 → 退单 → 销卡。App 经 CGS 网关([[svc_cgs]])调 PPC([[svc_ppc]]);PPC 出向调卡组织(YSE/Jaywan),入向接收卡组织/物流回调。本流程是卡产品的业务骨架,接口清单/错误码/用例指引见 [[reference_ppc_card_apis]],状态机与转换用例见 [[scn_card_lifecycle_transitions]]。

> 注:Jaywan(Dgpay 渠道)的预付卡有独立的供应商集成实现,见 [[flow_jaywan_prepaid_card]] 与 [[reference_jaywan_mbank_integration]]。

## 步骤(跨系统)
1. **开卡**:App → [[svc_cgs]] → [[svc_ppc]] 申请虚拟卡(`apply-virtual`)。前置 KYC 通过、已设支付密码;PPC 创建 [[tbl_ppc_t_virtual_card]] 记录(status=A),出向调 YSE/Jaywan 申请。卡组织发卡成功回调 → status=U。
2. **激活**:用户输入 ProxyNumber/OTP 并核身 → `activate`,status=U→N;期间设置 PIN(`set-pin`,PIN 加密)。
3. **消费授权**:卡组织 Authorization 回调(`/ppc/yse/notify/auth`)→ PPC 校验余额、写授权流水、设置 Pending Account。`ResponseCode=75` 表示 PIN locked。
   - Salary Card 域内五段式:Acquirer→UAESWITCH→Jaywan→Botim/YSE→PPC;国际跨境走 Mastercard 既有框架(见 [[reference_salary_card_cobadge]])。
4. **清算入账**:卡组织 Clearing/Settle 回调(`/ppc/yse/notify/clearing`)→ Pending Account 推进到 Settle / Refund / Reversal。
5. **退款 / 退单(chargeback)**:交易类型枚举 `T/S/R/RL/F/CB/RF/FRL`;退单业务背景见 [[reference_jaywan_mbank_integration]] 的 Chargeback 章节。
6. **锁 / 解锁卡**:`lock` / `unlock`(status N↔L);PIN locked 后调 APIPTR(Reset PIN)解除。
7. **实体卡链路**:`init-apply-physical`→`apply-physical`→支付(trade 回调)→ PPC 推 YSE 制卡 → 配送(USP/Jeebly 回调)→ `activate`。配送状态由 Jeebly Delivery Status 回调驱动。
8. **销卡**:`close`(status N/L→CI),前置余额=0、待结算清空、余额同步完成,否则 `NON_ZERO_BALANCE`;卡组织确认关卡回调 → status=CI→C。dormant cleanup 静默批量停用仅处理 MC 卡。

## 关联关系
- **经过的服务(有序)**:App → [[svc_cgs]] → [[svc_ppc]] → 卡组织(YSE/Jaywan,待补对象);trade / USP / Jeebly / grc 等上下游(待补对象)。(= `related_services` 取已存在的 svc_cgs / svc_ppc)
- **关键表**:[[tbl_ppc_t_virtual_card]](= `related_tables`)。
- **关键场景**:[[scn_card_lifecycle_transitions]](= `related_scenarios`)。

## 校验点
- 各状态流转后 [[tbl_ppc_t_virtual_card]].status 正确(见 [[scn_card_lifecycle_transitions]])。
- 授权占用 Pending Account → 清算推进到最终态;账务一致性(授权流水 vs 清算 vs 余额)。
- 关卡资损红线:非零余额禁止关卡;销卡后任何操作必拒。
- 异步回调幂等 + 乱序兜底对账(Authorization / Clearing / Jeebly)。
- 实体卡配送 7 天红线(Cancelled / RTO Delivered 后重下)。

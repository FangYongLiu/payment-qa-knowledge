---
id: scn_wps_sif_vs_paf
object_type: Scenario
name: WPS SIF 与 PAF 公司类型差异化发薪
aliases: [SIF vs PAF, WPS process_type 分支]
domain: wps
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/2272428082
tags: [wps, sif, paf, process_type]
related_services: [svc_payroll_core_service]
related_tables: [tbl_bps_t_corporate, tbl_bps_t_payroll_source]
related_logs: []
---

# WPS SIF 与 PAF 公司类型差异化发薪

> WPS 产品按 `bps.t_corporate.process_type` 区分两类公司:**SIF**(默认完整端到端产品)与 **PAF**(仅作为发薪通道的变体)。两者在发薪流程、发票模块、公司结构、专用数据表上有本质差异,是 WPS 的关键 QA 分支。

## 触发 / 入口
- 入口:企业入驻时选择/被分配的公司类型,落库 `bps.t_corporate.process_type`(取值 `SIF` / `PAF`)。
- 发薪入口:SIF 经 WPS portal 发起并审批;PAF 由 YSE 侧驱动,无 portal 发薪。

## 关联关系
- **涉及服务**:[[svc_payroll_core_service]](= `related_services`)。完整协作链路(YSE / [[svc_ppc]] / CBUAE / [[svc_tradeii]])见 [[flow_wps_company_onboarding_to_payroll]]。
- **校验的表**:[[tbl_bps_t_corporate]](`process_type` 区分字段)/ [[tbl_bps_t_payroll_source]](SIF 发薪主表;PAF 专用表见下)(= `related_tables`)。
- **相关日志**:待补。
- **端到端流程**:[[flow_wps_company_onboarding_to_payroll]]。

## 前置条件
- 企业已完成 onboarding,`bps.t_corporate` 已落库且 `process_type` 已确定。

## 操作步骤
1. 读取 `bps.t_corporate.process_type` 判定公司类型。
2. **SIF(默认产品)**:
   - 门户发薪:企业通过 WPS portal 发起并审批 payroll。
   - 发票模块:启用 invoice / billing(`bps.t_corp_invoice_config`、`bps.t_corp_invoice`/`_item` 等)。
   - 走完整协作链路(YSE / PPC / CBUAE / TradeII)。
   - 单公司结构。
   - Payroll 落 [[tbl_bps_t_payroll_source]](+ `_bulk` / `_data` 等)。
3. **PAF(变体,仅作发薪通道)**:
   - 无门户发薪:企业不通过 WPS portal 触发发薪。
   - 无发票模块:不使用 invoice / billing 配置。
   - 线下结算(offline settlement)。
   - YSE 驱动发薪:发薪由 YSE 侧驱动,而非企业门户。
   - 父/子公司结构(parent / sub-company)。
   - Payroll 落专用表 `bps.t_payroll_paf` / `t_payroll_paf_detail`(与 SIF 区分;Table 对象待补)。

## DB 校验点
- `bps.t_corporate.process_type` 取值与公司实际流程一致。
- SIF:`bps.t_payroll_source`/`_bulk`/`_data` 有数据,且 invoice 相关表(`t_corp_invoice*`)启用。
- PAF:`bps.t_payroll_paf`/`_detail` 有数据,且无 invoice 模块数据。

## 预期结果
- SIF 公司经门户发薪 + 发票闭环;PAF 公司线下结算、YSE 驱动、无门户/无发票,数据分别落各自专用表。

## 速查对照
| 维度 | SIF | PAF |
|---|---|---|
| 门户发薪 | ✅ | ❌ |
| 发票模块 | ✅ | ❌ |
| 结算方式 | 在线(TradeII 等) | 线下 |
| 发薪驱动方 | 企业门户 | YSE |
| 公司结构 | 单公司 | 父/子公司 |
| Payroll 表 | `t_payroll_source` / `_bulk` / `_data` 等 | `t_payroll_paf` / `_detail` |

> 不确定 / 缺失的点标「待补」,留待人工补充更新。

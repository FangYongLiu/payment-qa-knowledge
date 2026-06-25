---
id: tbl_bps_t_payroll_source
object_type: Table
name: WPS 薪资发放源表(bps.t_payroll_source)
aliases: [t_payroll_source]
domain: wps
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/2272428082
tags: [wps, payroll]
related_services: [svc_payroll_core_service]
related_scenarios: [scn_wps_sif_vs_paf]
---

# WPS 薪资发放源表(bps.t_payroll_source)

## 用途
SIF(默认产品)发薪流程的源数据表,记录 payroll 批次的来源数据。在 Create payroll 阶段落库(见 [[flow_wps_company_onboarding_to_payroll]])。PAF 公司使用专用表 `bps.t_payroll_paf` / `_detail`,不走本表(差异见 [[scn_wps_sif_vs_paf]])。

通用发薪相关表(同链路,Table 对象待补):`bps.t_payroll_source` 的 `_bulk` / `_data`、`bps.t_salary_load_command` / `_execute`、`bps.t_cb001_transfer_record`、`bps.t_salary_load_record`。央行文件:`bps.t_esa_file_record` / `_detail`(Non-Listed LRAs 的 EIF / WIF)。

## 关联关系
- **所属服务**:[[svc_payroll_core_service]](= frontmatter `related_services`,tbl→service 边)。
- **谁读写它**:WPS 发薪执行链路(YSE / [[svc_tradeii]] 执行资金划转,经 [[svc_ppc]] 转发)。
- **哪些场景校验它**:[[scn_wps_sif_vs_paf]](= `related_scenarios`)。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| ... | 待补 | 待补:原文未提供 |

## 主键 / 索引
- 待补:原文未提供。

## 校验点(QA 关注)
- SIF 公司发薪数据正确落 `t_payroll_source`/`_bulk`/`_data`;PAF 公司则落 `t_payroll_paf`/`_detail`,不污染本表。
- 发薪经 WPS(央行文件 SIF/PIF/PRC/DIF)或 Direct Transfer 路径,门户审批后由 YSE/TradeII 执行,资金划转与状态回写一致。
- **不确定 / 缺失的列与索引标「待补」,留给人工补充更新。**

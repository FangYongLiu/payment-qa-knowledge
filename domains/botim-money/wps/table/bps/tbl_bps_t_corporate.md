---
id: tbl_bps_t_corporate
object_type: Table
name: WPS 企业主表(bps.t_corporate)
aliases: [t_corporate]
domain: wps
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/2272428082
tags: [wps, company, corporate]
related_services: [svc_payroll_core_service]
related_scenarios: [scn_wps_sif_vs_paf]
---

# WPS 企业主表(bps.t_corporate)

## 用途
存储 WPS 企业(corporate)入驻后的主数据,是公司维度的核心表。决定公司类型与发薪流程分支的关键字段 `process_type`(SIF / PAF)位于此表。在 company onboarding 阶段落库(见 [[flow_wps_company_onboarding_to_payroll]])。

关联子表(同属公司维度,Table 对象待补):`bps.t_corporate_profile` / `_account` / `_address` / `_mohre`;IBAN 落 `vis.t_virtual_account`。

## 关联关系
- **所属服务**:[[svc_payroll_core_service]](= frontmatter `related_services`)。
- **谁读写它**:WPS 发薪/入驻链路服务(待补精确映射)。
- **哪些场景校验它**:[[scn_wps_sif_vs_paf]](= `related_scenarios`,按 `process_type` 分支)。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| process_type | 待补 | 公司类型,取值 `SIF` / `PAF`,决定发薪流程分支(见 [[scn_wps_sif_vs_paf]]) |
| 其它列 | 待补 | 待补:原文未提供 |

## 主键 / 索引
- 待补:原文未提供。

## 校验点(QA 关注)
- `process_type` 取值与公司实际流程一致(SIF 走门户+发票;PAF 线下+YSE 驱动)。
- 入驻审核通过后是否正确注册到 YSE 并获得 IBAN(IBAN 落 `vis.t_virtual_account`)。
- **不确定 / 缺失的列与索引标「待补」,留给人工补充更新。**

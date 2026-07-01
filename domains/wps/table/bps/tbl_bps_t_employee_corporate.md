---
id: tbl_bps_t_employee_corporate
object_type: Table
name: WPS 企业员工主表(bps.t_employee_corporate)
aliases: [t_employee_corporate]
domain: wps
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/2272428082
tags: [wps, employee]
related_services: [svc_payroll_core_service]
related_scenarios: []
---

# WPS 企业员工主表(bps.t_employee_corporate)

## 用途
WPS 员工维度的主表,持有员工状态(status)。在 Add employee 阶段落库(见 [[flow_wps_company_onboarding_to_payroll]]):员工以 EID 或 Passport 登记,类型为 Botim Wallet 或 Bank Account,经 Basis 审核后通过 YSE-CSPREG 同步到 YSE。

关联表(同属员工维度,Table 对象待补):`bps.t_employee` / `_profile`(含 `qr_code`)/ `_salary_account`(`card_ref_mid`/`vid`、IBAN、routing)/ `_address`;护照 KYC 资料 `bps.t_employee_kyc_material`。

## 关联关系
- **所属服务**:[[svc_payroll_core_service]](= frontmatter `related_services`)。
- **谁读写它**:WPS 员工注册/发薪链路服务(待补精确映射)。
- **哪些场景校验它**:待补(EID vs Passport 员工注册场景待建)。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| status | 待补 | 员工状态(主表持有);Passport 用户初始状态 `KYCVerification` |
| 其它列 | 待补 | 待补:原文未提供 |

## 主键 / 索引
- 待补:原文未提供。

## 校验点(QA 关注)
- 员工注册路径正确:EID vs Passport、Botim Wallet vs Bank Account。
- Passport 用户初始 status 为 `KYCVerification`,卡激活时必须走 QR-code 路径才能进入 Passport KYC。
- 经 YSE-CSPREG 同步后状态是否正确回写。
- **不确定 / 缺失的列与索引标「待补」,留给人工补充更新。**

---
id: flow_merchant_open_wps
object_type: Flow
domain: merchant-management
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:tester/462749700
tags:
- WPS
- 开通
- 审核
subdomain: null
module: null
sensitivity: normal
name: 商户开通WPS流程
aliases: []
related_services: []
related_tables:
- merchant.t_common_audit_order
- merchant.t_merchant_biz_open
- merchant.t_biz_admin_info
- merchant.t_merchant_wps_info
- merchant.t_staff
- merchant.t_staff_role
- member.tr_member_account
- vis.t_virtual_account
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
商户在 Unified Portal 申请开通 WPS 业务，由 Basis 审核通过后完成 WPS 业务数据落库的端到端流程。审核通过后会创建 WPS 业务信息、业务管理员、员工角色、WPS 工资基本账户及虚拟账户(Initial)。Uat 环境下需手动推进 Iban。

## 步骤(跨系统)
1. **Unified Portal 申请开通 WPS**
   - 接口：`api/acquiring/secure/merchant2/bizOpen/wps`
   - 请求数据体：`bizAdminList`，`wpsInfoList`
   - 数据落库：
     - `merchant.t_common_audit_order` 商户公共审核(待审核)
2. **Basis 审核通过 WPS**
   - 数据落库：
     - Merchant 商户库
       - `merchant.t_common_audit_order` 商户公共审核 -- `audit_result:PASS`
       - `merchant.t_merchant_biz_open` 商户开通业务 -- `["Acquire","WPS"]`
       - `merchant.t_biz_admin_info` 商户业务管理员 -- `["SUPPER_ADMIN","ACQUIRE_ADMIN","WPS_ADMIN"]`
       - `merchant.t_merchant_wps_info` 商户 WPS 业务信息
       - `merchant.t_staff` 商户员工信息
       - `merchant.t_staff_role` 商户员工角色
     - Member 会员库
       - `member.tr_member_account` 基本账户 -- `WPS_SALARY`
     - Vis
       - `vis.t_virtual_account` 虚拟账户 -- `Status:Initial`
3. **Uat 环境补充**：手动推进 Iban。

## 涉及服务/表
- Merchant 商户库
  - `merchant.t_common_audit_order`
  - `merchant.t_merchant_biz_open`
  - `merchant.t_biz_admin_info`
  - `merchant.t_merchant_wps_info`
  - `merchant.t_staff`
  - `merchant.t_staff_role`
- Member 会员库
  - `member.tr_member_account`(`WPS_SALARY`)
- Vis
  - `vis.t_virtual_account`(`Status:Initial`)

## 校验点
- `merchant.t_common_audit_order.audit_result` = `PASS`
- `merchant.t_merchant_biz_open` 开通业务包含 `WPS`(可与已有 `Acquire` 共存为 `["Acquire","WPS"]`)
- `merchant.t_biz_admin_info` 包含 `WPS_ADMIN`(以及 `SUPPER_ADMIN`/`ACQUIRE_ADMIN`)
- `merchant.t_merchant_wps_info` 已生成 WPS 业务信息
- `member.tr_member_account` 存在 `WPS_SALARY` 基本账户
- `vis.t_virtual_account.Status` = `Initial`
- Uat 环境需手动推进 Iban

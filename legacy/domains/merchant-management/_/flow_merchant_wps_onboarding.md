---
id: flow_merchant_wps_onboarding
object_type: Flow
domain: merchant-management
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:34ef57ae-73fe-4cd4-a064-e8edfb238167
tags:
- WPS
- onboarding
- merchant
subdomain: null
module: null
sensitivity: normal
name: 商户WPS开通端到端流程
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
描述商户从 Unified Portal 申请开通 WPS 业务，到 Basis 审核通过后正式开通 WPS 的端到端流程。前置条件：商户已完成 Acquire 开通（参见 [[flow_merchant_acquire_onboarding]]），因为 WPS 通常基于已有商户主体新增开通。

## 步骤(跨系统)
1. **Unified Portal 申请开通 WPS**
   - 调用接口：`api/acquiring/secure/merchant2/bizOpen/wps`（参见 [[api_merchant_bizopen_wps]]）
   - 请求数据体：`bizAdminList`、`wpsInfoList`
   - 落库：`merchant.t_common_audit_order`（生成商户公共审核单）

2. **Basis 审核通过 WPS**
   - 审核通过后落库变更：
     - `merchant.t_common_audit_order` — `audit_result: PASS`
     - `merchant.t_merchant_biz_open` — 商户开通业务追加 `WPS`，最终为 `["Acquire","WPS"]`
     - `merchant.t_biz_admin_info` — 商户业务管理员追加 `WPS_ADMIN`，最终为 `["SUPPER_ADMIN","ACQUIRE_ADMIN","WPS_ADMIN"]`
     - `merchant.t_merchant_wps_info` — 写入商户 WPS 业务信息
     - `merchant.t_staff`、`merchant.t_staff_role` — 商户员工与角色信息
     - `member.tr_member_account` — 新增基本账户类型 `WPS_SALARY`
     - `vis.t_virtual_account` — 虚拟账户，`Status: Initial`

3. **UAT 环境**
   - 手动推进 Iban

## 涉及服务/表
- 商户库 Merchant：
  - `merchant.t_common_audit_order`（商户公共审核）
  - `merchant.t_merchant_biz_open`（商户开通业务）
  - `merchant.t_biz_admin_info`（商户业务管理员）
  - `merchant.t_merchant_wps_info`（商户 WPS 业务信息）
  - `merchant.t_staff`（商户员工信息）
  - `merchant.t_staff_role`（商户员工角色）
- 会员库 Member：
  - `member.tr_member_account`（基本账户 `WPS_SALARY`）
- 虚拟账户库 Vis：
  - `vis.t_virtual_account`（虚拟账户 `Status: Initial`）

## 校验点
- 申请阶段是否在 `merchant.t_common_audit_order` 生成审核单。
- Basis 审核通过后 `audit_result` 应为 `PASS`。
- `merchant.t_merchant_biz_open` 是否包含 `WPS`。
- `merchant.t_biz_admin_info` 是否包含 `WPS_ADMIN` 角色。
- `merchant.t_merchant_wps_info` 是否写入业务信息。
- `member.tr_member_account` 是否生成 `WPS_SALARY` 基本账户。
- `vis.t_virtual_account` 是否生成且初始状态为 `Initial`。
- UAT 环境需手动推进 Iban 才能完成完整链路验证。

---
id: api_merchant_bizopen_wps
object_type: API
domain: merchant-management
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:tester/462749700
tags:
- WPS
- 开通业务
subdomain: null
module: null
sensitivity: normal
name: 商户开通WPS接口
aliases: []
related_services: []
related_tables:
- merchant.t_common_audit_order
- merchant.t_merchant_biz_open
- merchant.t_biz_admin_info
- merchant.t_merchant_wps_info
- merchant.t_staff
- merchant.t_staff_role
related_scenarios:
- flow_merchant_open_wps
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
已注册商户在 Unified Portal 提交申请，开通 WPS 业务，提交后进入商户公共审核流程，待 Basis 审核通过后落库 WPS 业务相关数据。

## 路径/方法
- 路径：`api/acquiring/secure/merchant2/bizOpen/wps`
- 来源：Unified Portal

## 入参
请求数据体：
- `bizAdminList`
- `wpsInfoList`

## 出参
原文未提供。

## 错误码
原文未提供。

## 测试校验点
- 接口提交后，`merchant.t_common_audit_order`(商户公共审核)生成审核单。
- Basis 审核通过(`audit_result:PASS`)后核对：
  - `merchant.t_common_audit_order`：audit_result=PASS
  - `merchant.t_merchant_biz_open`：包含 ["Acquire","WPS"]
  - `merchant.t_biz_admin_info`：包含 ["SUPPER_ADMIN","ACQUIRE_ADMIN","WPS_ADMIN"]
  - `merchant.t_merchant_wps_info`：商户 WPS 业务信息落库
  - `merchant.t_staff`、`merchant.t_staff_role`：员工与员工角色落库
  - `member.tr_member_account`：基本账户类型 `WPS_SALARY`
  - `vis.t_virtual_account`：虚拟账户 Status=Initial
- UAT 环境需手动推进 Iban。

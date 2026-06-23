---
id: api_merchant_bizopen_wps
object_type: API
domain: portal-operations
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:34ef57ae-73fe-4cd4-a064-e8edfb238167
tags:
- WPS
- 商户开通
- 开通业务
subdomain: merchant-onboarding
module: null
sensitivity: normal
name: 商户开通WPS接口
aliases: []
related_services:
- svc_merchant
---

## 用途
Unified Portal 提交申请，为已注册的商户开通 WPS 业务。提交后进入商户公共审核流程，待 Basis 审核通过后落库 WPS 业务相关数据。

## 路径/方法
- 路径：`/api/acquiring/secure/merchant2/bizOpen/wps`
- 鉴权：secure（已登录态）
- 来源：Unified Portal

## 入参
请求数据体包含：
- `bizAdminList`：商户业务管理员列表
- `wpsInfoList`：WPS 业务信息列表

## 出参
原文未提供。

## 错误码
原文未提供。

## 测试校验点
提交后涉及数据库写入与审核流程：

- 接口提交后：
  - `merchant.t_common_audit_order`：商户公共审核记录被创建（待审核）

- Basis 审核通过 WPS 后核对：
  - `merchant.t_common_audit_order`：`audit_result` = `PASS`
  - `merchant.t_merchant_biz_open`：商户开通业务包含 `["Acquire","WPS"]`
  - `merchant.t_biz_admin_info`：商户业务管理员包含 `["SUPPER_ADMIN","ACQUIRE_ADMIN","WPS_ADMIN"]`
  - `merchant.t_merchant_wps_info`：商户 WPS 业务信息落库
  - `merchant.t_staff`：商户员工信息落库
  - `merchant.t_staff_role`：商户员工角色落库
  - `member.tr_member_account`：基本账户类型 `WPS_SALARY`
  - `vis.t_virtual_account`：虚拟账户创建（Status: Initial）

- UAT 环境下 Iban 需手动推进。
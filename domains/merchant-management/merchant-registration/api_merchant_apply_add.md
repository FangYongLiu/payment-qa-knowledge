---
id: api_merchant_apply_add
object_type: API
domain: merchant-management
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:tester/462749700
tags:
- merchant
- apply
- acquire
- wps
subdomain: merchant-registration
module: null
sensitivity: normal
name: 申请商户接口
aliases: []
related_services: []
related_tables:
- merchant.t_merchant_creation_order
- merchant.t_merchant
- merchant.t_merchant_address
- merchant.t_partner
- merchant.t_binding_card_apply_info
- merchant.t_merchant_biz_open
- merchant.t_biz_admin_info
- merchant.t_merchant_acquire_info
- merchant.t_staff
- merchant.t_staff_role
- member.tm_member
- member.tm_member_identity
related_scenarios:
- flow_merchant_register_acquire
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
用于商户注册申请，由 Unified Portal 等来源提交申请，可开通业务 Acquire 或 WPS。

## 路径/方法
- 路径：`/api/acquiring/permitAll/merchant/apply/add`
- 鉴权层级：permitAll（无需登录态）

## 入参
请求数据体包含字段：
- `acquireInfoList`
- `addressList`
- `bindingCard`
- `bizAdminList`
- `merchantData`
- `partnerList`
- `signatory`
- `wpsInfoList`

## 出参
原文未给出。

## 错误码
原文未给出。

## 测试校验点
申请提交后，校验以下数据库写入：

- Merchant 商户库
  - `merchant.t_merchant_creation_order` 商户创建信息
  - `merchant.t_merchant` 商户信息
  - `merchant.t_merchant_address` 地址列表，类型为 `["register","business"]`
  - `merchant.t_partner` 合作伙伴信息
  - `merchant.t_binding_card_apply_info` 绑卡信息
  - `merchant.t_merchant_biz_open` 商户开通业务，值为 `["Acquire","WPS"]`
  - `merchant.t_biz_admin_info` 商户业务管理员，角色 `["SUPPER_ADMIN","ACQUIRE_ADMIN","WPS_ADMIN"]`
  - `merchant.t_merchant_acquire_info` 商户 Acquire 业务
  - `merchant.t_staff` 商户员工信息
  - `merchant.t_staff_role` 商户员工角色
- Member 会员库
  - `member.tm_member` 会员信息，状态 0 未激活
  - `member.tm_member_identity` 会员标识，状态 0 未激活

注：申请提交后会员状态为未激活（0），需 Basis 审核通过 Acquire 后才推进至激活态。

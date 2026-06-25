---
id: api_merchant_apply_add
object_type: API
domain: portal-operations
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:34ef57ae-73fe-4cd4-a064-e8edfb238167
tags:
- acquire
- apply
- merchant
- wps
subdomain: merchant-onboarding
module: null
sensitivity: normal
name: 商户申请新增接口
aliases: []
related_services:
- svc_merchant
related_tables: [tbl_member_tm_member, tbl_member_tm_member_identity]
---

## 用途
Unified Portal 等来源提交商户申请,用于新增商户注册并开通业务(Acquire 或 WPS)。落库商户创建信息、商户信息、地址、合作伙伴、绑卡、业务开通、业务管理员、员工角色,以及会员库的未激活会员与会员标识。

## 路径/方法
- 路径:`/api/acquiring/permitAll/merchant/apply/add`
- 鉴权层级:permitAll(无需登录态)
- 来源入口:Unified Portal
- 开通业务范围:`Acquire` 或 `WPS`

## 入参
请求数据体字段:
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
申请提交后需校验以下数据库落库情况:

### Merchant 商户库
- `merchant.t_merchant_creation_order` 商户创建信息
- `merchant.t_merchant` 商户信息
- `merchant.t_merchant_address` 地址列表,类型包含 `["register","business"]`
- `merchant.t_partner` 合作伙伴信息
- `merchant.t_binding_card_apply_info` 绑卡信息
- `merchant.t_merchant_biz_open` 商户开通业务,取值 `["Acquire","WPS"]`
- `merchant.t_biz_admin_info` 商户业务管理员,角色 `["SUPPER_ADMIN","ACQUIRE_ADMIN","WPS_ADMIN"]`
- `merchant.t_merchant_acquire_info` 商户 Acquire 业务
- `merchant.t_staff` 商户员工信息
- `merchant.t_staff_role` 商户员工角色

### Member 会员库
- `member.tm_member` 会员信息,状态 `0 未激活`
- `member.tm_member_identity` 会员标识,状态 `0 未激活`

注:申请提交后会员状态为未激活(0),需 Basis 审核通过 Acquire 后才推进至激活态。
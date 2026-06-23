---
title: 商户管理总览
domain: merchant-management
kind: wiki_page
slug: merchant-management-overview
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:tester/462749700
tags: []
---

# 商户管理总览

本页概述商户在统一控台体系中的注册来源、申请入口，以及 Acquire / WPS 两类业务的开通与审核流转脉络。详细数据库表清单见 [[merchant-registration-data-tables]]。

## 商户注册来源

商户注册可来自以下渠道：

- Unified Portal
- Agent
- Basis
- Botim
- 统一控台

## Acquire 业务开通

### 申请阶段（Unified Portal 提交申请）

- 入口接口：`/api/acquiring/permitAll/merchant/apply/add`，详见 [[api_merchant_apply_add]]
- 可开通业务：`Acquire` 或 `WPS`
- 请求数据体字段：
  - `acquireInfoList`
  - `addressList`
  - `bindingCard`
  - `bizAdminList`
  - `merchantData`
  - `partnerList`
  - `signatory`
  - `wpsInfoList`
- 完整提交流程见 [[flow_merchant_register_acquire]]

### 审核阶段（Basis 审核通过 Acquire）

审核通过后，关键状态推进：

- `t_merchant_creation_order.Status` → `ENABLED`
- `t_merchant.Status` → `MERCHANT_ENABLED`
- 会员相关：`tm_member`、`tm_member_identity` 状态由 `0 未激活` 变为 `1 激活`
- 落地基本账户 `BASIC`、受益人卡信息、商户协议、对账单配置以及 Merchant VAM Topup 产品申请/订单等

## WPS 业务开通

### 申请阶段（Unified Portal 申请开通 WPS）

- 入口接口：`api/acquiring/secure/merchant2/bizOpen/wps`，详见 [[api_merchant_bizopen_wps]]
- 请求数据体字段：
  - `bizAdminList`
  - `wpsInfoList`
- 申请落入 `merchant.t_common_audit_order` 进入公共审核
- 完整开通流程见 [[flow_merchant_open_wps]]

### 审核阶段（Basis 审核通过 WPS）

- `t_common_audit_order.audit_result` → `PASS`
- `t_merchant_biz_open` 业务集合更新为 `["Acquire","WPS"]`
- 业务管理员角色：`SUPPER_ADMIN`、`ACQUIRE_ADMIN`、`WPS_ADMIN`
- 写入 `t_merchant_wps_info`、商户员工与角色信息
- 会员侧落地 `WPS_SALARY` 基本账户
- VIS 侧创建虚拟账户 `vis.t_virtual_account`，初始 `Status: Initial`
- UAT 环境需手动推进 Iban

## 涉及的数据存储

商户注册与业务开通涉及多库协作：`Merchant` 商户库、`Member` 会员库、`ppcenter` 产品中心库、`dpm` 会员账户库、`statementii` 账单库、`contract` 合同库、`vis` 虚拟账户库。各表用途与状态值参见 [[merchant-registration-data-tables]]。

## 角色与状态枚举

- 商户业务管理员角色：`SUPPER_ADMIN`、`ACQUIRE_ADMIN`、`WPS_ADMIN`
- 地址类型：`["register","business"]`
- 商户开通业务类型：`["Acquire","WPS"]`
- 会员状态：`0 未激活` / `1 激活`
- 商户/创建单状态：`MERCHANT_ENABLED` / `ENABLED`
- 审核结果：`PASS`
- 虚拟账户初始状态：`Initial`

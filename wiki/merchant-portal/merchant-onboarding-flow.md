---
title: 商户注册与入驻流程
domain: merchant-portal
kind: wiki_page
slug: merchant-onboarding-flow
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/997785804
tags: []
---

# 商户注册与入驻流程

本页描述商户从首次注册、登录到提交入驻信息、选择业务类型，并最终经 BMOC 后台审核完成激活的完整链路。该流程跨多个服务，全部成功后商户才可正式使用。详见 [[flow_merchant_onboarding]]。

## 入口与测试账号

商户注册/登录入口为 Unified Portal，环境信息：

| 环境 | 地址 | OTP 说明 |
|---|---|---|
| Sim | https://sim-web-unified.test2pay.com/verify/login | 默认 `161616` |
| Uat | https://uat-web-unified.test2pay.com/verify/login | 需要 real OTP |

通用测试账号：
- Mobile：`+971-556579167`
- Password：`132580` 或 `Yong0324####`

## 业务流程概览

商户入驻是一个跨系统流程，涉及以下服务，任一环节失败都会阻塞商户激活：

- **Member**：全局用户身份服务，管理个人/企业会员账号，提供 Member ID。
- **Merchant**：商户域服务，管理商户档案、入驻状态、商户–会员关系、生命周期。
- **Basis**：核心基础服务，处理账户启用、产品激活、运营审核与内部配置。
- **AML**：反洗钱合规与风险筛查，AML 失败将阻止商户激活。
- **VIS**：虚拟 IBAN 创建与管理。
- **Billing**：账单账户创建、订单初始化、结算配置。
- **Contract**：商户合同生成与管理。
- **Unified Portal**：注册与入驻表单的前端入口。

各服务及对应 owner 详见 [[merchant-onboarding-service-map]]。

## 注册与登录

- 首次注册默认通过 **OTP 登录**，登录后必须设置密码。
- Sim 环境 OTP 固定为 `161616`；Uat 必须使用真实 OTP。
- 注册成功后，使用 Administrator 信息中的手机号登录 Portal，该号码具有 **administrator role**。

## 入驻表单填写

在 Onboarding 表单中填写公司基础信息及银行账户信息，其中：

- **Company Bank Account / IBAN**：测试值 `AE790030013112189920001`
- IBAN 字段会经过后端服务校验。

## 业务类型选择

`Company Business Type` 决定后续可用功能：

- **Payment**：即 Merchant Acquire Service，进入收单商户控台流程，参见 [[acquire-merchant-console-guide]]。
- **WPS**：另一类业务（Wage Protection 类）。

Administrator Information 中填入的手机号即为后续登录 Portal 的管理员账号。

## BMOC 审核（Merchant Status Approval）

入驻提交后需在 BMOC 后台完成人工/系统审核，商户状态才会从待审核流转为可用。

- 登录地址：`https://sim-admin.corp.test2pay.com/basis-cas/login?service=https://sim-admin.corp.test2pay.com/bmoc/cas`
- 菜单路径：**Basis Merchant => Business => Merchant => Merchant Onboarding**

审核步骤：

1. **Step 1**：完成 AML Risk Calculate（反洗钱风险计算）。
2. **Step 2**：完成 KYB Approval（企业资质审核）。

系统处理完成后，回到列表查看 Merchant Status 是否已变更为激活态。

## 数据落库要点

入驻流程会写入 Merchant、Member、Ppcenter、Dpm、Statementii、Contract、Vis 等多个数据库的表。完整影响范围与字段含义见 [[merchant-onboarding-database-scope]]。关键起点表：

- `merchant.t_merchant_creation_order`：入驻申请单
- `merchant.t_merchant`：商户主信息
- `merchant.t_merchant_biz_open`：已开通的业务类型
- `merchant.t_biz_admin_info`：管理员信息

## 相关页面

- [[merchant-portal-overview]]：Merchant Portal 总体功能与定位。
- [[merchant-portal-env-access-guide]]：DB / Redis / Kibana 等环境访问。
- [[flow_acquire_product_application]]：选择 Payment 后续的产品申请审核流程。

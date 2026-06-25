---
id: ref_bmoc_basis_merchant
object_type: reference
name: BMOC / Basis Merchant 运营后台菜单与权限指南
aliases: [bmoc, basis merchant menu, 运营后台, botim money operations center]
domain: portal-operations
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: 'wiki:e02c9096, wiki:d3d9d62f, confluence:AQ/1310621839'
tags: [bmoc, basis-merchant, console, operations, approval, permissions]
related_services: [svc_basis_merchant]
---

# BMOC / Basis Merchant 运营后台菜单与权限指南

> **BMOC**(Botim Money Operation Console)是 PayBy 内部运营管理后台;**Basis Merchant** 是其中聚焦商户运营的系统，覆盖商户全生命周期审批与配置。控台标识 `PAYBY BASIS`(顶部 "WELCOME TO PAYBY")。后台由 [[svc_basis_merchant]] 承载。适用人群:测试、产品、开发、运营。

## 控台入口与登录
- 地址见 [[ref_portal_env_access]](Sim/UAT/Prod basis-merchant、BMOC)。
- 登录需**员工域账号**(示例 `fangyong.liu` / `Can Wang`);账号问题找 OPS: wei.li，角色权限由 QA 在 `Permissions` 添加。
- 左侧主导航分 GENERAL / BUSINESS / TMS;Basis Merchant 相关菜单位于 `BUSINESS > Merchant`。

## 菜单结构总览(按功能分类)
| 功能分类 | 主要菜单项 | 说明 |
| --- | --- | --- |
| 商户管理 | Merchant Management | 查询/编辑商户资料、设置结算信息 |
| 商户入驻与开通 | Onboarding Management、Open Product、Merchant Approval、Application Approval | 开户审核、产品申请 |
| 渠道配置 | Fund Provider Management、3rd Party MID | 收单通道、上送渠道信息 |
| 设备管理 | TMS > Device Approval / Activated Devices | POS 审批、终端状态 |
| 员工门店管理 | Member Config、Store Management、Staff Management、Cashier Management | 门店/员工/收银员权限 |
| 报表与对账 | Statements、Reconciliation、Reconciliation Summary / Clear Flow / Fund Flow | 结算账单、异常调账 |
| 权限与日志 | Permissions、Operate Log、Staff 2FA Unbind | 角色配置、操作日志、2FA 解绑 |
| 税务与公告 | Tax Invoice、Tax Info Approval、Announcements | 税务审批/报表、控台通知 |
| 银行账户 | Bank Account Approval | 商户银行账户审核 |

`BUSINESS > Merchant` 子菜单:Merchant Approval、Application Approval、Tax Info Approval、Staff Management、Store Management、Cashier Management、Reconciliation、Statements、Staff 2FA Unbind、Tax Invoice、Announcements、Bank Account Approval。

## 核心菜单:商户入驻审核

### Onboarding Management
- 路径:`/BUSINESS/Merchant/Merchant Onboarding/Onboarding Management`
- 用途:审批商户注册申请(资料校验、资质上传、产品选择)。
- 流程:搜索待审核商户 → 查看详细资料页 → 审核通过 / 驳回 / 修改配置。完整入驻链路见 [[flow_merchant_onboarding]]。

### Merchant Approval
- 入口:`BUSINESS > Merchant > Merchant Approval`，是商户审批主工作页。
- 筛选:Merchant ID、Agent Mid、Merchant Name、Contact Mobile、状态(默认 ALL)、类型(All Type)、来源(All Source)、Search、`+ New Merchant`。
- 列表字段:Apply ID、Source(如 `AGENT`/`PORTAL`)、Merchant ID、Merchant Name、Contact Mobile、Application Time、Status(如 `Awaiting Approval`)、Action(View / Approval / Add Staff)。
- 操作:按 Source 区分代理商/门户自助提交;View 看详情;Approval 进审核;Add Staff 补录员工。

## General Audit(配置审核)
- 商户配置变更(如收支分离 `fee_b`)走 General Audit:先生成 Audit Record，审核人执行 Audit 后生效。
- 入口:`General Audit → Audit Record`，按 `AuditId` 搜索/排序，默认 10 条/页;每条 `View`，待审记录额外 `Audit` 弹窗(`AuditInfo` 区 `MerchantId`/`ParamKey` 只读)。
- 收支分离配置详见 [[scn_merchant_fee_bearer_separation]]。

## 权限与账号管理
- 角色与权限在 `Permissions` 配置，操作记录通过 `Operate Log` 留痕;员工 2FA 异常用 `Staff 2FA Unbind` 解绑。
- 建议按岗位(测试/运营/产品/开发)最小化授权，敏感操作(商户审核、调账、设备审批)受控授权。

## 常见问题
- 看不到子菜单:先确认域账号已开通，且对应菜单已在 `Permissions` 授权;`BUSINESS > Merchant` 一级模块需被授权展开。
- 控台访问/角色分配问题:先查域账号是否开通。

## 关联
- 内部运营后台另有常用 Portal(VIP/缓存/用户解绑/短信/收银台鉴权/系统管理-用户/角色/部门/字典/菜单/登录与操作日志等)的导航布局，作为后台通用模块速查。
- 环境与登录入口见 [[ref_portal_env_access]];入驻流程见 [[flow_merchant_onboarding]]。

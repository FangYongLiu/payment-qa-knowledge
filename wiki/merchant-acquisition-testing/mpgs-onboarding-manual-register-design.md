---
title: MPGS Onboarding 手动报备技术方案
domain: merchant-acquisition-testing
kind: wiki_page
slug: mpgs-onboarding-manual-register-design
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:7c033704-1056-4e5a-9598-3d67ba9edba4
tags: []
---

# MPGS Onboarding 手动报备技术方案

为支持 MPGS E-com 快速上线、规避 Visa 对 Game merchant 封禁风险，引入"线下在 MPGS Onboarding Portal 完成报备 + 结果回写 Payby"的人工录入能力。本页描述该能力的背景、系统改动、领域设计、流程方案与实现选型。

## 背景与目标

- 业务背景：MPGS E-com 需快速上线，结合当前商户数量，采用线下在 MPGS Onboarding Portal 报备的方式。
- 关联需求：MPGS Onboarding [Awaiting Review]
- 目标：支持手动报备能力，将商户在外部供应商处登记的信息同步回 Payby 系统。

## 系统改动范围

涉及 onboarding 与 basis 两个服务：

- onboarding 服务
  - 报备规则管理模块支持配置登记类型（系统自动、人工录入），本次新增"人工录入"。
  - 新增手动报备信息入口，支持商户、门店、设备的信息写入。
- basis 服务
  - 页面支持配置登记类型；登记页面支持人工录入信息进行报备。

## 供应商配置：登记类型选择

在 FundProvider 配置中新增"登记类型"选择项，支持选择 `自动报备` 或 `手动录入`。

接口变更见 [[api_onboarding_get_fund_provider_config]]：

- 返回字段新增 `registerType`，标识供应商登记类型。
- 当 `registerType = Manual` 时，`onboardingRuleList` 为空。

## 数据库变更

### t_fund_provider 增加 register_type 字段

参见 [[tbl_onboarding_t_fund_provider]]。

```sql
ALTER TABLE `onboarding`.`t_fund_provider`
ADD COLUMN `register_type` varchar(50) NOT NULL DEFAULT 'SYSTEM_AUTO'
  COMMENT '报备类型，SYSTEM_AUTO、MANUAL'
```

枚举：`SYSTEM_AUTO`、`MANUAL`，默认 `SYSTEM_AUTO`。

### 新增人工登记规则相关表

- [[tbl_onboarding_t_manual_register_rule]]：人工登记规则表，按 `(fund_provider_code, type)` 唯一。
- [[tbl_onboarding_t_manual_register_rule_field]]：人工登记字段配置表，按 `(rule_id, name)` 唯一，记录字段名与是否必填（`mandatory`）。

## 人工录入信息登记

### 流程概述

- 商户登记流程：在 Onboarding Management 页面提供 edit / sync 入口，进入人工录入弹窗。
- 人工录入流程：弹窗根据规则展示字段 → 用户录入 → 提交 → 写入登记结果。

### 接口变更

新增 [[api_onboarding_manual_register]] `manualRegister` 接口：

- 用于人工录入数据方式提交报备信息。
- 接口内部将录入的数据转换为登记 `item` 与 `item_result_map` 数据进行存储。
- 若上报数据字段中 `key` 已存在对应数据，则覆盖。

### 实现方案选型

| 方案 | 实现方式 | 评估 | 是否采用 |
|---|---|---|---|
| 方案一 复用商户自动报备流转逻辑 | 在自动报备流程中兼容手动报备逻辑，通过逻辑隔离不同模式行为 | 自动/手动逻辑耦合，后续状态流转可能不一致，互相影响 | 不考虑 |
| 方案二 Onboarding 订单中增加上报方式属性 | 订单新增上报类型，自动上报仅处理自动类型订单；写入成功后订单置为成功 | 可较好隔离两种流程，后续扩展互不影响 | 否 |
| 方案三 仅写入报备结果信息 | 收到请求后直接写入 `item` 与 `item_result_param`，设置为激活状态；写入失败抛错由上游重试 | 实现轻量，对原自动上报无影响；缺点是未维护 OnboardingOrder，无法查看登记记录（OnboardingOrder 未对外暴露） | 采用 |

选型说明：人工上报场景中商户已在外部供应商完成注册，上报仅用于将信息回传 Payby，故采用方案三。

## 任务拆分与排期

后端：
- 人工录入配置接口开发：1.5 人/天
- 人工录入数据写入开发：1 人/天

前端：
- FundProvider 人工录入配置规则页面流程开发：1 人/天
- FundProvider Query 页面展示人工录入结果（状态为激活），预计无开发量待确认
- Onboarding Management 页面支持展示 edit / sync 入口：0.5 人/天
- 人工录入弹窗展示与提交逻辑开发：2 天

联调：
- 前后端联调：1.5 人/天

排期：9.13–9.14，9.25–9.30。

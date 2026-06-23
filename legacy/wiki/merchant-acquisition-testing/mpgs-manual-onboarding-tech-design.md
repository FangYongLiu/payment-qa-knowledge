---
title: MPGS手动报备技术方案
domain: merchant-acquisition-testing
kind: wiki_page
slug: mpgs-manual-onboarding-tech-design
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/684425357
tags: []
---

# MPGS手动报备技术方案

为支持 MPGS E-com 快速上线、规避 Visa 对 Game merchant 封禁风险，本方案在现有 Onboarding 体系内新增「人工录入」报备能力：商户先在 MPGS Onboarding Portal 线下完成登记，再将结果同步回 Payby 系统。

## 背景与目标

- 业务诉求：MPGS Onboarding 处于 Awaiting Review 阶段时，需要一种线下报备 + 信息回传的通路。
- 目标：在 onboarding/basis 服务中扩展手动报备能力，支持商户、门店、设备的信息写入。

## 系统改动点

- **onboarding 服务**
  - 报备规则管理模块支持配置登记类型：`SYSTEM_AUTO`（系统自动）、`MANUAL`（人工录入）。
  - 新增手动报备信息入口，支持商户/门店/设备数据写入。
- **basis 服务**
  - 页面支持配置登记类型。
  - 登记页面支持以人工录入方式提交报备信息。

## 功能设计

### 供应商配置 - 登记类型

- FundProvider 配置新增「登记类型」选择：自动报备 / 手动录入。
- 配置查询接口 [[api_onboarding_get_config]] 返回 `registerType` 标识供应商登记类型；当 `registerType = Manual` 时 `onboardingRuleList` 为空。

### 人工录入信息登记

- 用例覆盖：商户登记管理、人工录入弹窗 UI 流程、人工录入提交业务流程。
- 端到端流转参见 [[flow_mpgs_manual_onboarding]]。
- 写入接口：[[api_onboarding_manual_register]]，由前端弹窗提交人工录入数据，后端转换为登记 item 与 item_result_map 数据。

## 数据库变更

- 资金供应商表 [[tbl_onboarding_t_fund_provider]] 增加 `register_type` 字段：

```sql
ALTER TABLE `onboarding`.`t_fund_provider`
ADD COLUMN `register_type` varchar(50) NOT NULL DEFAULT 'SYSTEM_AUTO'
COMMENT '报备类型，SYSTEM_AUTO、MANUAL';
```

- 新增人工登记规则表 [[tbl_onboarding_t_manual_register_rule]]。
- 新增人工登记字段配置表 [[tbl_onboarding_t_manual_register_rule_field]]。

## 方案选型

| 方案 | 实现方式 | 评估 | 是否采用 |
|---|---|---|---|
| 方案一：复用自动报备流转逻辑 | 在自动报备流程中兼容手动报备逻辑，通过逻辑隔离不同模式 | 自动/手动逻辑耦合，复杂且可能相互影响（后续状态流转可能不一致） | 不考虑 |
| 方案二：Onboarding 订单新增上报方式属性 | 订单中新增上报类型，自动上报仅处理 `自动上报` 类型订单；写入成功后订单状态置为成功 | 隔离自动/手动流程，后续扩展互不影响 | 备选 |
| 方案三：仅写入报备结果信息 | 收到手动报备请求后，直接写入 item 与 item_result_param 并置为激活；写入失败抛错由上游重试 | 实现轻量，对原自动上报无影响；缺点：未维护 OnboardingOrder，无法查看登记记录（OnboardingOrder 未对外暴露） | **采用** |

选型结论：人工上报场景中商户已在外部供应商处完成注册，回传只是把信息同步到 Payby，故采用方案三。

## 接口变更

- 配置查询：[[api_onboarding_get_config]] 返回 `registerType`。
- 人工录入：新增 [[api_onboarding_manual_register]]，接口内部将录入数据转换为登记 item、item_result_map 数据进行存储；同 key 已存在数据时进行覆盖。

## 任务拆分与排期

**后端**
- 人工录入配置接口开发：1.5 人/天
- 人工录入数据写入开发：1 人/天

**前端**
- FundProvider 人工录入配置规则页面流程开发：1 人/天
- FundProvider Query 页面展示人工录入结果（状态为激活），预计无开发量待确认
- Onboarding Management 页面支持展示 edit sync 入口：0.5 人/天
- 人工录入弹窗展示与提交逻辑开发：2 天

**联调**
- 前后端联调：1.5 人/天

**排期**：9.13–9.14、9.25–9.30。

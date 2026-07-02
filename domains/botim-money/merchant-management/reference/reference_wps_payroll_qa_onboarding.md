---
id: reference_wps_payroll_qa_onboarding
object_type: Reference
name: WPS Payroll QA 三周入职计划
aliases: [wps payroll qa onboarding, wps 入职, qa onboarding plan]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: 'wiki:b9c47ea9-7a47-4cf2-9849-6bc4dfdabc97, confluence:AQ/2252570627'
tags: [wps, payroll, onboarding, qa, training]
related_services: []
---

# WPS Payroll QA 三周入职计划

> WPS Payroll QA 新人入职整体规划:角色范围、三周时间线(Guided → Semi-independent → Independent)、评估方式。通过入职=能独立支持 WPS Payroll QA 并把一个 ticket 推到 release。联系人:Xinwei Cao。

## 角色范围
WPS Payroll QA 主要参与:Company registration & approval flows、Employee registration(Add Employee)、Payroll creation & disbursement(WPS via CBUAE 及 Direct Transfer)、Invoice/billing verification、Test case writing & bug reporting。聚焦发薪场景及背后集成:YSE via PPC、CBUAE file exchange、TradeII。

## 时间线
| 阶段 | 周 | 主题 |
| --- | --- | --- |
| Guided | Week 1 | Foundations、WPS 知识、guided ticket |
| Semi-independent | Week 2 | 在轻度指导下主导一个 ticket |
| Independent | Week 3 | 独立 own 一个 ticket 到 release |

评估结果:✅ Pass / ⚠️ High Risk / ❌ Fail，由 mentor 评审并记录到 Wiki。

## Week 1 — 基础与 WPS 入门(Guided)
- **目标**:开通所有 QA 账号/权限;掌握 WPS 四大核心流程;熟悉相关库表与状态检查;在指导下完整跑一个 ticket(写用例→评审→执行→报 bug→关单)。
- **Day 1**:团队介绍 + 账号开通(Jira、Zephyr、Confluence、BMOC SIM/UAT、WPS portal、DB 工具;basis-merchant 菜单权限);理解 SIM vs UAT 用途。
- **权限到位前(Day1-2)**:读 WPS 知识库(company registration、invoice config、add employee、create payroll、company management)、理解 YSE(via PPC)/CBUAE 角色、读近期 Zephyr 用例 + 1-2 个历史 Jira ticket 全生命周期。
- **通过标准**:能讲清 WPS 四大核心流程;完成并执行一个已评审通过的 ticket 级用例;知道在哪些库表核对、在哪查日志。

## Week 2 — 半独立带单(Semi-Independent)
- 独立主导一张 ticket，团队仅在被询问时回答、不主动推进;独立读需求/写用例、在 Zephyr 关联执行/独立提 bug;练习何时/向谁提问(环境、需求歧义、集成方 YSE/CBUAE/TradeII)。评审比 Week 1 轻量(关注结果与判断)。
- **预期**:最少干预下完成一张 ticket，用例与执行基本可独立成立。

## Week 3 — 独立执行与发布(Independent)
- 完全 own 一个 ticket:requirement → test cases → execution → bug reporting → sign-off → release/go-live;主动与 Dev/PM/stakeholder 对齐;自管进度与 issue 闭环;判断何时 sign-off / 何时拉 review。团队只在发布前 final review/sign-off。发布后 debrief(做得好/待改进/下一步如 PAF-type companies、CBUAE file flows、partner integration testing)。
- **预期**:独立交付并上线一个 ticket，达团队标准，测试结论清晰可靠、文档完备。

> 发布流程见 [[reference_payby_release_process]];WPS 业务开通链路见 [[flow_merchant_onboarding]]。

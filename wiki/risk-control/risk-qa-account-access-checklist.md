---
title: 风控QA账号与访问权限清单
domain: risk-control
kind: wiki_page
slug: risk-qa-account-access-checklist
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2161541121
tags: []
---

# 风控QA账号与访问权限清单

入职第一天（Day 1）需要完成的全部账号开通与访问权限设置清单，包括登录入口、申请联系人和验收标准。本页是 [[risk-qa-week1-onboarding-plan]] 的 Day 1 配套手册。

## 目标与通过标准

- 完成所有 QA 必需账号与访问权限的开通
- 无账号阻塞问题
- 知道账号异常时如何处理
- 能够清晰识别 QA / Dev / Ops / PMO 的关键联系人

## 账号与访问清单

### IPA 账号
- 登录入口：`https://ipa1.corp.algento.com/ipa/ui/`
- 使用企业域账号修改密码（参考 New Employee Onboarding Email Guide）
- 联系人（Ops）：zhiqi.jin@astratech.ae

### VPN 访问
- VPN 地址：`20.74.221.9:443`
- 联系人（Ops）：zhiqi.jin@astratech.ae

### JIRA 账号
- 登录入口：`https://algento.atlassian.net/jira/your-work`
- 使用 AstraTech 邮箱登录
- 验收标准：可访问 `PAYM-2755`
- 联系人：
  - Ops：zhiqi.jin@astratech.ae
  - PMO：Bilal.Javed@astratech.ae

### Wiki 账号
- 登录入口：`https://algento.atlassian.net/wiki/home`
- 使用 AstraTech 邮箱登录
- 验收标准：可访问 Wiki 空间 `https://algento.atlassian.net/wiki/spaces/AQ`

### CI/CD 平台
- 登录入口：`https://appcenter-new.corp.payby.com/#/index`
- 使用域账号登录
- 验收标准：login success
- 联系人（QA）：ext_Nitesh.Parasher@astratech.ae

### BMOC Portal 访问
- SIM 环境：`https://sim-admin.corp.test2pay.com/bmoc/`
- UAT 环境：`https://uat-admin.corp.test2pay.com/bmoc/`
- 验收标准：login success
- 联系人（QA）：ext_Nitesh.Parasher@astratech.ae

### GitLab 访问
- 入口：`https://gitlab.test2pay.com/qa/cgs-apitest`
- 使用域账号登录
- 验收标准：可访问 db project 链接
- 联系人（DBA）：Li.Zhang@astratech.ae

## 团队介绍与关键联系人

| 角色 | 联系人 |
|---|---|
| QA | ext_Nitesh.Parasher@astratech.ae |
| Ops | zhiqi.jin@astratech.ae |
| PMO | Bilal.Javed@astratech.ae |
| DBA | Li.Zhang@astratech.ae |

> 后续 Day 2 起还需开通 Basis Admin（`uat.intra.azure.test2pay.com/bigdata-admin/`）、AstraShield、Kibana、MongoDB（`grc` / `aml` / `bigdata` 库读权限），由 Risk Dev（chao.li@astratech.ae、Abhimanyu.Singh@astratech.ae）授权，详见 [[risk-qa-week1-onboarding-plan]]。

## 相关链接

- 入职整体计划：[[risk-qa-week1-onboarding-plan]]
- 风控架构总览：[[risk-system-architecture-overview]]

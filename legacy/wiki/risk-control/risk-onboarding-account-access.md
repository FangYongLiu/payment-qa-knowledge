---
title: 风控QA入职账号与权限清单
domain: risk-control
kind: wiki_page
slug: risk-onboarding-account-access
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:00c6a300-c75b-4c5d-b0c9-c18e010dfb50
tags: []
---

# 风控QA入职账号与权限清单

Day1 入职首日需完成的所有账号开通与权限申请清单，覆盖 IPA / VPN / JIRA / Wiki / CI/CD / BMOC / GitLab，并标明每项的对接人与验收标准。本页为 [[risk-onboarding-week1-plan]] 的 Day1 配套清单。

## 总体目标

- 完成所有 QA 必需账号与访问权限的开通
- 无账号阻塞问题，且了解账号异常时的处理路径
- 熟悉团队 QA / Dev / Product / PMO 关键联系人

## 账号与访问开通清单

### IPA Account
- 入口：`https://ipa1.corp.algento.com/ipa/ui/`
- 使用企业域账号登录，按 New Employee Onboarding Email Guide 修改密码
- 对接人 (Ops)：zhiqi.jin@astratech.ae

### VPN Access
- VPN 地址：`20.74.221.9:443`
- 对接人 (Ops)：zhiqi.jin@astratech.ae

### JIRA Account
- 入口：`https://algento.atlassian.net/jira/your-work`
- 使用 AstraTech 邮箱登录
- 验收：能访问 `PAYM-2755`
- 对接人：
  - Ops：zhiqi.jin@astratech.ae
  - PMO：Bilal.Javed@astratech.ae

### Wiki Account
- 入口：`https://algento.atlassian.net/wiki/home`
- 使用 AstraTech 邮箱登录
- 验收：能访问 Wiki 空间 `https://algento.atlassian.net/wiki/spaces/AQ`

### CI/CD Platform
- 入口：`https://appcenter-new.corp.payby.com/#/index`
- 使用域账号登录
- 验收：登录成功
- 对接人 (QA)：ext_Nitesh.Parasher@astratech.ae

### BMOC Portal Access
- SIM 环境：`https://sim-admin.corp.test2pay.com/bmoc/`
- UAT 环境：`https://uat-admin.corp.test2pay.com/bmoc/`
- 验收：登录成功
- 对接人 (QA)：ext_Nitesh.Parasher@astratech.ae

### GitLab Access
- 入口：`https://gitlab.test2pay.com/qa/cgs-apitest`
- 使用域账号登录
- 验收：能访问 DB 项目链接
- 对接人 (DBA)：Li.Zhang@astratech.ae

## 团队介绍与关键联系人

入职首日同步完成 QA / Dev / Product / PMO 团队成员介绍，确保能清晰识别各方关键联系人。

- QA：ext_Nitesh.Parasher@astratech.ae
- Ops：zhiqi.jin@astratech.ae
- PMO：Bilal.Javed@astratech.ae
- DBA：Li.Zhang@astratech.ae

## 验收标准 (Passing Criteria)

- 所有上述账号均无登录 / 访问阻塞问题
- 知晓账号异常时的对接人与处理路径

## 后续访问

Day2 起还需进一步申请的业务后台访问（Basis Admin / AstraShield / Kibana / MongoDB 读权限等）属于 Day2 范围，详见 [[risk-onboarding-week1-plan]]，对应后台与系统说明参见 [[auto_basis_visual_rule_admin]] 与 [[risk-system-architecture-overview]]。

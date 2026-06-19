---
title: ChargeBack邮件相关配置
domain: risk-control
kind: wiki_page
slug: chargeback-mail-config
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/1333395487
tags: []
---

# ChargeBack邮件相关配置

本页汇总 ChargeBack 邮件发送所依赖的系统参数配置项，包括总开关、白名单、各类默认收件地址等。配置路径统一位于 `Basis → RISK CONTROL → Data Analysis → Risk System Param`，修改后需刷新缓存。具体的发送判断逻辑见 [[chargeback-mail-notification]]。

## 配置入口

- 路径：`Basis → RISK CONTROL → Data Analysis → Risk System Param`
- 注意：参数变更后需要 **刷缓存** 才能生效

## 邮件相关参数

| 参数 Key | 用途 | 取值/格式 |
|---|---|---|
| `chargeback_mail_send_outer_switch` | 邮件总开关 | yes / no |
| `chargeback_send_mail_product_config` | 业务产品码白名单 | 业务产品码1, 业务产品码2… |
| `chargeback_mail_send_to_default` | 默认邮件地址 | 邮件地址1, 邮件地址2… |
| `chargeback_mail_send_external_default` | 外部邮件地址 | 邮件地址1, 邮件地址2… |
| `chargeback_mail_send_psp_default` | PSP 默认邮件地址（PSP 默认 6 邮箱） | 邮件地址1, 邮件地址2… |
| `chargeback_mail_receiver_partner_XXXX` | 按 PartnerName 配置的收件邮箱 | 目前主要用于 remittance 渠道 |

## 关键开关说明

- `chargeback_mail_send_outer_switch`：控制是否走"默认邮件"短路逻辑
  - `Yes`：仅发送 `chargeback_mail_send_to_default` 配置的默认邮箱
  - `No`：进入按商户类型/ReferredId/External/PartnerName 等条件的完整判断流程
- `chargeback_send_mail_product_config`：业务产品码白名单，仅命中白名单的产品码才进入邮件发送流程
- `chargeback_mail_receiver_partner_XXXX`：以 PartnerName 为后缀的动态 Key，用于按渠道（如 remittance）配置专属收件人

## 与冻结相关的配置

ChargeBack 冻结亦受 Risk System Param 的白名单控制（详见 [[chargeback-freeze-logic]]）：

- `chargeback_ignore_frozen_merchant_list`：冻结白名单，名单内的商户 ID 将忽略自动冻结

## 相关页面

- 邮件发送判断顺序与各 TS 场景：[[chargeback-mail-notification]]
- 邮件发送场景测试集：[[scn_chargeback_mail_send_cases]]
- ChargeBack 业务总览：[[chargeback-business-overview]]

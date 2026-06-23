---
title: ChargeBack相关配置参数
domain: risk-control
kind: wiki_page
slug: chargeback-config-params
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:b45ef58e-e6ac-4d48-9837-7307c6d42c4e
tags: []
---

# ChargeBack相关配置参数

本页汇总 ChargeBack 业务在 `Risk System Param` 中的相关配置项，包括邮件总开关、白名单、默认/外部/PSP 邮箱以及 PartnerName 等。配置路径统一为：`Basis → RISK CONTROL → Data Analysis → Risk System Param`，更改后需刷新缓存。

## 配置入口

- 路径：`Basis → RISK CONTROL → Data Analysis → Risk System Param`
- 修改后需 **刷缓存** 生效

## 邮件相关配置

用于控制 ChargeBack 邮件发送行为，详见 [[chargeback-mail-notification]]。

| 配置项 | 含义 | 取值/格式 |
|---|---|---|
| `chargeback_mail_send_outer_switch` | 邮件总开关 | yes / no |
| `chargeback_send_mail_product_config` | 业务产品码白名单 | 业务产品码1, 业务产品码2… |
| `chargeback_mail_send_to_default` | 默认邮件地址 | 邮件地址1, 邮件地址2… |
| `chargeback_mail_send_external_default` | 外部邮件地址 | 邮件地址1, 邮件地址2… |
| `chargeback_mail_send_psp_default` | PSP 邮件地址（PSP 默认 6 个邮箱） | 邮件地址1, 邮件地址2… |
| `chargeback_mail_receiver_partner_XXXX` | PartnerName 配置 | 目前主要用于 remittance 渠道 |

说明：
- `chargeback_mail_send_to_default` 同时也作为邮件发送场景判定中的 "邮件开关" 字段使用（Yes 时直接发默认配置邮箱）。
- `chargeback_mail_receiver_partner_XXXX` 中的 `XXXX` 对应具体 partner_name，正常商户场景较少匹配。

## 冻结白名单配置

用于跳过 ChargeBack 自动冻结的商户名单，详见 [[chargeback-freeze-logic]]。

- 配置项：`chargeback_ignore_frozen_merchant_list`
- 含义：名单内的 merchantId 将 **忽略冻结**
- 仅对 New case 触发的冻结流程生效

## 关联说明

- 邮件配置项的实际生效顺序与场景组合参见 [[chargeback-mail-notification]] 与 [[scn_chargeback_mail_send_cases]]
- 整体业务背景参见 [[chargeback-business-overview]]

---
title: ChargeBack邮件通知收件人路由逻辑
domain: acquire-transaction
kind: wiki_page
slug: chargeback-email-notification-routing
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:3d08fe2a-dc35-4f64-a990-564c2037ea5e
tags: []
---

# ChargeBack邮件通知收件人路由逻辑

ChargeBack 场景下，系统根据邮件开关、商户类型（PSP/非PSP/外部）以及 ReferredId、partner_name 等关联信息，逐层判定最终的邮件收件人集合。

## 入口：邮件开关检查

- 首先判断 **邮件开关是否开启**。
- 若 **开启**：直接 **发送至默认配置邮箱**，流程结束。
- 若 **关闭**：进入商户类型分支判断。

## 商户类型分支

邮件开关关闭后，按 **商户类型** 分流：

- **PSP商户**：进入 ReferredId / PSP 邮箱判定。
- **非PSP商户**：进一步判断是否为外部商户。

## PSP商户路由

先判断 **是否存在 ReferredId**：

- **存在 ReferredId**：
  - **ReferredId 对应邮箱存在** → 发送至 **ReferredId邮箱 + PSP默认6邮箱 + 默认邮箱**
  - **ReferredId 对应邮箱不存在** → 回退判断 **PSP商户自身邮箱**：
    - 存在 → 发送至 **PSP商户邮箱 + PSP默认6邮箱 + 默认邮箱**
    - 不存在 → 发送至 **PSP默认6邮箱 + 默认邮箱**
- **不存在 ReferredId**：直接判断 **PSP商户自身邮箱**：
  - 存在 → 发送至 **PSP商户邮箱 + PSP默认6邮箱 + 默认邮箱**
  - 不存在 → 发送至 **PSP默认6邮箱 + 默认邮箱**

## 非PSP商户路由

判断 **是否为外部商户**：

- **是外部商户**：进一步判断 **是否存在 partner_name**：
  - 存在 → 发送至 **partner_name** 对应的邮箱（按原文流程指向该分支的收件人配置）。
  - （以下分支原文截断，未给出完整终点。）

## 关键判定要素

- **邮件开关**：决定是否进入精细化路由。
- **商户类型**：PSP商户 / 非PSP商户（含外部商户）。
- **ReferredId**：PSP 场景下优先级最高的邮箱来源。
- **PSP商户自身邮箱**：ReferredId 缺失或无邮箱时的回退来源。
- **PSP默认6邮箱 + 默认邮箱**：PSP 分支下始终附加的兜底收件人。
- **partner_name**：外部商户场景下用于定位收件人。

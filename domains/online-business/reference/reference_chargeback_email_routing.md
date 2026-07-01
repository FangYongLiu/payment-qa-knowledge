---
id: reference_chargeback_email_routing
object_type: Reference
name: ChargeBack 邮件通知收件人路由逻辑
aliases: [chargeback email routing, 拒付邮件通知]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: wiki_image
source_ref: wiki_image:3d08fe2a (ChargeBack邮件通知收件人路由逻辑)
tags: [online-business, acquiring, chargeback, notification, email]
related_services: [svc_acquireii]
---

# ChargeBack 邮件通知收件人路由逻辑

> ChargeBack(拒付)场景下,系统按邮件开关 → 商户类型 → ReferredId/partner_name 等逐层判定最终收件人集合。QA 测拒付通知时的判定真值表。
> 注:与 [[scn_online_business_chargeback_file_intake]] / [[flow_chargeback_file_processing]](拒付文件入库处理)是不同环节——本页只讲**邮件收件人路由**。

## 入口:邮件开关
- **开启** → 直接发送至**默认配置邮箱**,流程结束。
- **关闭** → 进入商户类型分支。

## 商户类型分支(邮件开关关闭后)
- **PSP 商户** → 进 ReferredId / PSP 邮箱判定。
- **非 PSP 商户** → 判断是否外部商户。

## PSP 商户路由
先判断**是否存在 ReferredId**:
- **存在 ReferredId**:
  - ReferredId 对应邮箱存在 → 发 **ReferredId邮箱 + PSP默认6邮箱 + 默认邮箱**。
  - ReferredId 对应邮箱不存在 → 回退判 PSP 商户自身邮箱:
    - 存在 → **PSP商户邮箱 + PSP默认6邮箱 + 默认邮箱**。
    - 不存在 → **PSP默认6邮箱 + 默认邮箱**。
- **不存在 ReferredId** → 直接判 PSP 商户自身邮箱:
  - 存在 → **PSP商户邮箱 + PSP默认6邮箱 + 默认邮箱**。
  - 不存在 → **PSP默认6邮箱 + 默认邮箱**。

## 非 PSP 商户路由
判断是否外部商户:
- **是外部商户** → 判断是否存在 `partner_name`:
  - 存在 → 发至 partner_name 对应邮箱。
  - 不存在 → 原文流程截断,标「待补:原文未给出完整终点」。

## 关键判定要素
- **邮件开关**:决定是否进入精细化路由。
- **商户类型**:PSP / 非PSP(含外部商户)。
- **ReferredId**:PSP 场景优先级最高的邮箱来源。
- **PSP 商户自身邮箱**:ReferredId 缺失或无邮箱时的回退。
- **PSP默认6邮箱 + 默认邮箱**:PSP 分支始终附加的兜底收件人。
- **partner_name**:外部商户场景定位收件人。

## 关联关系
- **涉及服务**:[[svc_acquireii]] 收单(= `related_services`)。

## QA 关注点
- PSP × ReferredId 有无 × 邮箱有无 的全组合收件人断言。
- 兜底收件人(PSP默认6 + 默认)在各分支始终附加。
- 外部商户 partner_name 缺失分支待业务补全终点。

---
id: domain_marketing
object_type: Domain
name: marketing
aliases: [营销, 增长, 积分, 优惠券, promo]
domain: marketing
business_line: botim-money
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-24'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: [marketing, 营销, 增长, 积分, 优惠券, coupon, promo]
related_services: [svc_marketing, svc_coupon_service, svc_gptrade, svc_green_points, svc_coupon_gateway, svc_marketnotify, svc_gpoint, svc_coupon, svc_marketing_gateway, svc_marketing_campaign, svc_marketing_event, svc_promo_campaign, svc_promo_engine, svc_promo_gateway, svc_promo_merchant]
---

# marketing(营销 / 增长 / 积分)

> 业务域总览。营销/增长业务线:营销活动、优惠券、积分、促销。域 lead 待指定。

## 概述
Marketing 营销/增长业务域:营销活动与网关(marketing/event/campaign/gateway)、营销通知
(marketnotify)、优惠券(coupon/service/gateway)、积分(green-points/gpoint/gptrade)、
促销(promo-campaign/engine/gateway/merchant)。此前散落在 payment-core 与 wallet,现统一收拢。

## 覆盖范围
- 营销(payment-core 迁入):marketing、marketing-event、marketing-campaign、marketing-gateway、marketnotify
- 优惠券(payment-core 迁入):coupon、coupon-service、coupon-gateway
- 积分(payment-core 迁入):green-points、gpoint、gptrade
- 促销(wallet 迁入):promo-campaign、promo-engine、promo-gateway、promo-merchant

## QA 关注点
- 待补。
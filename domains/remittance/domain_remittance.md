---
id: domain_remittance
object_type: Domain
name: remittance
aliases: [汇款]
domain: remittance
product: payment
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-06-24'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: [remittance, 汇款]
related_services: [svc_remittance, svc_remittance_swiftx, svc_remittance_bdo, svc_remittance_ime, svc_remittance_ext, svc_remittance_fuze, svc_remittance_platon, svc_remittance_trustbank, svc_remittance_fawry, svc_remittance_codepoint, svc_remittance_cbe, svc_remittance_jinglepay, svc_remittance_arp, svc_remittance_terrapay]
---

# remittance(汇款)

> 业务域总览(入口节点)。owner lei.pan。细节见各服务对象。

## 概述
汇款域:汇款核心与各汇款渠道(swiftx/bdo/ime/fuze/platon/trustbank/fawry/codepoint/cbe/jinglepay/arp/terrapay 等)。

## 覆盖范围
共 14 个服务:remittance、remittance-swiftx、remittance-bdo、remittance-ime、remittance-ext、remittance-fuze、remittance-platon、remittance-trustbank、remittance-fawry、remittance-codepoint、remittance-cbe、remittance-jinglepay、remittance-arp、remittance-terrapay。

## QA 关注点
- 待补。

## 流程 / 场景 / 排障 索引
本域 流程 / 场景 / 排障 / 自动化 对象索引:
- [[auto_remittance_remittance]](自动化:跨境汇款自动化)
- [[auto_remittance_vam]](自动化:VAM 虚拟账户自动化)
- [[flow_remittance_pix_mpc]](流程:PIX MPC 商户呈现码扫码支付端到端流程)
- [[flow_remittance_send_money]](流程:Send Money 端到端转账流程)
- [[scn_remittance_cross_border]](场景:跨境汇款 (Remittance))
- [[scn_remittance_rate_alert]](场景:汇率提醒(Rate Alert))
- [[scn_remittance_send_money]](场景:Send Money 转账(KYC 分支 / 退款 / 通知))

---
id: domain_channel
object_type: Domain
name: channel
aliases: [渠道, 收单渠道, qpay, 第三方处理器]
domain: channel
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-24'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: [channel, 渠道, qpay, 收单渠道]
related_services: [svc_qpay_ni_channel, svc_qpay_nipos, svc_qpay_niboarding, svc_qpay_installment, svc_qpay_npss, svc_qpay_fsii, svc_qpay_fs, svc_qpay_aplus, svc_qpay_pl_channel, svc_qpay_enbd, svc_qpay_klip, svc_qpay_mcii, svc_qpay_lean, svc_qpay_cko, svc_qpay_mpgs, svc_qpay_zand, svc_qpay_nisocket, svc_kiosk_channel, svc_3ds2, svc_bafl_channel]
---

# channel(渠道 / QPay 第三方处理器)

> 业务域总览。QPay 系列渠道接入(各第三方收单/支付处理器)。域 lead 待指定。
> 注:「收单(acquiring)」作为 online-business 的 subdomain;本域专指渠道接入实现。

## 概述
Channel 渠道域:QPay 系列渠道接入(NI/CKO/MPGS/ENBD/Zand/Lean/Klip 等第三方处理器)
与渠道核心(qpay-mcii/fs/fsii)。从 payment-tools 拆出为独立渠道域。

## 覆盖范围(payment-tools 迁入)
- 渠道核心:qpay-mcii、qpay-fs、qpay-fsii
- 渠道接入:qpay-pl-channel、qpay-installment、qpay-ni-channel、qpay-klip、qpay-cko、
  qpay-aplus、qpay-lean、qpay-nipos、qpay-nisocket、qpay-niboarding、qpay-mpgs、
  qpay-enbd、qpay-npss、qpay-zand

## QA 关注点
- 待补。

## 流程 / 场景 / 排障 索引
本域 流程 / 场景 / 排障 / 自动化 对象索引:
- [[flow_botim_payby_login]](流程:Botim-PayBy 服务端登录与 Token 刷新流程)
- [[flow_enbd_fundout]](流程:ENBD 渠道出款流程(含账户映射 / 余额监控))
- [[flow_mg_remittance]](流程:MG (MoneyGram) 汇款端到端流程)
- [[flow_pix_wechat_mpc_payment]](流程:PIX 微信 MPC 扫码支付端到端流程)
- [[flow_pix_wechat_reconciliation]](流程:PIX 微信渠道对账文件下载与自动对账流程)
- [[flow_pix_wechat_refund]](流程:PIX 微信渠道退款流程(含退款推定))
- [[flow_wechat_overseas_static_qr_payment]](流程:微信海外用户主扫静态码支付流程(EPCC))
- [[scn_botim_payby_integration]](场景:Botim-PayBy 服务端集成(gRPC 网关 / 加解密 / Bind Customer / UID 兼容 / Outbound API))
- [[scn_channel_prerelease_collaboration]](场景:PayBy 渠道发布前 Dev-Test-Product 协作流程(6 步))
- [[scn_cko_subscription_payment]](场景:CKO 订阅支付测试场景集(路由矩阵 + 渠道定义 + 测试指南))
- [[scn_gppc_dgpay_key_exchange]](场景:GPPC-DGPAY 渠道密钥交换与配置)
- [[scn_mg_prcss_risk_review]](场景:MG PRCSS 风控审核场景测试)
- [[scn_mpgs_onboarding]](场景:MPGS Onboarding 组件架构与数据模型)
- [[scn_pix_wechat_vendor_api]](场景:PIX 微信 MPC Vendor API 清单、配置与字段校验)
- [[ts_enbd_channel_balance_not_enough]](排障:ENBD 出款报 channel account balance is not enough)
- [[ts_mg_order_state_handling]](排障:MG 渠道订单状态映射与特殊处理(PRCSS/AFR/REFND/707))

---
id: flow_unionpay_card_issuance
object_type: Flow
name: UnionPay 银联卡开卡端到端流程
aliases:
- unionpay-card-issuance
- 银联卡开卡
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/1268580390; wiki:4e177d56-875e-413a-a120-94fb6aefb87b
tags:
- unionpay
- 开卡
- kyc
- escrow
- upic
related_services:
- svc_escrow
- svc_upic
related_tables: []
related_scenarios:
- scn_unionpay_usage
---

# UnionPay 银联卡开卡端到端流程

## 概述
用户完成 KYC 后,由 [[svc_escrow]] 系统向 [[svc_upic]] 应用推送通知,upic 调用银联接口为用户开通银联卡并将开卡记录落库。整个开卡过程对用户**无感知**(无声息),正常情况下不会失败,仅在网络异常时可能失败。开卡完成不等于可用——用户实际使用 UnionPay 功能前还需走激活流程(见 [[flow_unionpay_card_activation]])。

## 步骤(跨系统)
1. 用户完成 KYC。
2. [[svc_escrow]] 系统向 [[svc_upic]] 应用推送通知。
3. upic 接收到通知后,调用**银联接口**(外部)为用户开通银联卡。
4. 开卡成功后,将记录写入 `upic.t_upi_card`,状态为 `OS`。

## 关联关系
- **经过的服务(有序)**:[[svc_escrow]] → [[svc_upic]](= `related_services`)
- **外部接口**:银联开卡接口(外部,待补 svc 对象)
- **关键表**:`upic.t_upi_card`(开卡记录表,状态 `OS` 表示已开卡;原文未提供完整表结构,待补 tbl 对象)
- **关键场景**:[[scn_unionpay_usage]](= `related_scenarios`)

## 校验点
- 触发前提:用户已完成 KYC。
- 开卡成功后 `upic.t_upi_card` 中应存在记录,且状态为 `OS`。
- 用户无感知(无声息),无 UI 流程。
- 失败场景仅在网络异常时出现,正常情况不会失败。
- 开卡完成不等于可用,需后续激活(见 [[flow_unionpay_card_activation]])。

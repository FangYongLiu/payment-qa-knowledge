---
id: api_pix_mpc_get_rules
object_type: API
domain: remittance
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/517832723
tags:
- pix
- mpc
subdomain: pix
module: mpc
sensitivity: normal
name: 查询MPC匹配规则接口 (/pix/mpc/v1/get-rules)
aliases: []
related_services: []
related_tables: []
related_scenarios:
- flow_pix_mpc_payment
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
供 wallet 在扫码前获取商户呈现码（MPC, Merchant Presented Code）的匹配规则，用于本地匹配 QrCode。Wallet 可对返回的规则进行缓存，缓存有效期至少 2 天。

## 路径/方法
- 路径：/pix/mpc/v1/get-rules
- 所属系统：pix
- Dubbo 实现：MpcFacade.getMatchRules（pix-channel）

## 入参
原文未提供。

## 出参
- 返回 QrCode 的匹配规则列表
- 匹配规则类型（match rule type）包含：PREFIX

## 错误码
原文未提供。

## 测试校验点
- 接口能返回包含 PREFIX 类型在内的匹配规则
- Wallet 端可基于返回规则成功匹配 QrCode（参见后续 /pix/mpc/v1/parse 步骤）
- 缓存策略：wallet 对规则的缓存时长不少于 2 天
- Dubbo facade `MpcFacade.getMatchRules` 在 pix-channel 中的实现可被正确调用

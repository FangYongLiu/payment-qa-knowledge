---
id: api_pix_mpc_get_rules
object_type: API
domain: remittance
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:f244c1d0-438b-46a8-be70-acdc8cfa85b4
tags:
- pix
- mpc
subdomain: pix
module: mpc
sensitivity: normal
name: 获取商户码匹配规则接口 (/pix/mpc/v1/get-rules)
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
返回 MPC(Merchant Presented Code)二维码的匹配规则，供钱包(wallet)侧用于识别扫描到的二维码是否属于商户码。钱包可缓存返回的规则至少 2 天，避免每次扫码都调用。

## 路径/方法
- 路径：`/pix/mpc/v1/get-rules`
- 所属系统：pix
- 内部 dubbo facade 实现：`MpcFacade.getMatchRules`(由 pix-channel 实现)
- CGS API Doc：TODO(原文未给出详细签名)

## 入参
原文未给出，TODO。

## 出参
匹配规则列表，包含匹配规则类型(match rule type)：
- `PREFIX`：按前缀匹配二维码

其他字段原文未给出。

## 错误码
原文未给出。

## 测试校验点
- 接口返回的规则中应包含规则类型 `PREFIX`。
- 钱包侧应能将规则缓存至少 2 天，缓存期内不重复调用。
- 钱包使用返回的规则可正确匹配 MPC QrCode，匹配成功后再进入 `/pix/mpc/v1/parse` 流程。
- pix-channel 侧 `MpcFacade.getMatchRules` dubbo facade 已正确实现并被 pix 调用。

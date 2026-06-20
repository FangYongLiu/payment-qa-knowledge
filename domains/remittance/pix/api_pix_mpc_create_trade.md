---
id: api_pix_mpc_create_trade
object_type: API
domain: remittance
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: wiki:f244c1d0-438b-46a8-be70-acdc8cfa85b4
tags:
- MPC
- Pix
- create-trade
subdomain: pix
module: mpc
sensitivity: normal
name: 创建MPC交易接口 (/pix/mpc/v1/create-trade)
aliases:
- /pix/mpc/v1/create-trade
related_services: []
related_tables: []
related_scenarios:
- flow_pix_mpc_payment
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
在用户(可选)输入支付金额后，由 wallet 调用 pix 创建 MPC 交易。pix 侧基于费率(rate)配置对金额进行校验，并返回 cashierToken，供后续走既有收银台(cashier)支付流程使用。

## 路径/方法
- 路径：/pix/mpc/v1/create-trade
- 所属系统：pix
- 调用方：wallet
- 下游 dubbo facade：MpcFacade.parseCode (由 pix-channel 实现)
- 详细 CGS API Doc：TODO

## 入参
原文未给出字段级定义(CGS API Doc: TODO)。流程上下文中应包含：
- 上一步 /pix/mpc/v1/parse 返回的 code id (用于关联商户与交易/费率信息)
- (Optional) 用户输入的支付金额

## 出参
- cashierToken：用于进入既有 cashier 支付流程
- 其他字段：原文未列出 (CGS API Doc: TODO)

## 错误码
原文未列出，CGS API Doc: TODO。

## 测试校验点
- 金额校验：依据 rate 配置 (rate config) 对入参金额进行校验，超出/不符合规则应被拒绝
- 正常路径：成功创建交易并返回 cashierToken，wallet 可据此进入既有收银台支付流程
- 与 /pix/mpc/v1/parse 的衔接：使用 parse 返回的 code id 创建交易，商户与交易信息(含费率)一致
- 可选金额场景：用户未输入金额(若商户码本身已带金额)与用户输入金额(需用费率换算本币)两种分支均可创建成功
- 后续衔接：返回的 cashierToken 能驱动 cashier 支付流程，并可被 /pix/mpc/v1/query-trade 查询到对应交易
- dubbo 实现：底层走 MpcFacade.parseCode (pix-channel) 实现可达

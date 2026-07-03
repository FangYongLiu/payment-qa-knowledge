---
id: reference_open_api_developer_portal
object_type: Reference
name: Botim Money 开放 API 开发者门户 (developers.botim.money)
aliases: [open api, developer portal, developers.botim.money, 开放API, 对外API文档]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-03'
source_type: reference
source_ref: 'https://developers.botim.money/docs/ (对外公开开放 API 门户, fetched 2026-07-03)'
tags: [online-business, acquiring, SGS, open-api, developer-portal, 对外契约]
related_services: [svc_sgs, svc_acquireii]
related_scenarios: [scn_online_business_openapi_protocol_signing]
---

# Botim Money 开放 API 开发者门户 (developers.botim.money)

商户 / 合作方对外集成 Botim Money 收单能力的**官方公开 API 文档门户**:<https://developers.botim.money/docs/>。这是外部合作方实际对接的**权威对外契约**;仓库内各 `api_sgs_acquire_*` 对象是内部视角(源自内部接口文档 v2.25 + Confluence),二者应保持一致——**冲突时以本门户的公开契约为准**(它是对外承诺的版本)。

> QA 用途:对外集成/合作方联调用例、签名与协议校验、接口契约回归(公开文档变更即对外契约变更)。写收单对外用例时以本门户 + [[reference_acquire_protocol_and_codes]] 为准。

## 环境与接入
| 项 | 值 |
| --- | --- |
| 联调(UAT) base | `https://uat.test2pay.com` |
| 生产 base | `https://api.payby.com` |
| 收单接口前缀 | `/sgs/api/acquire2/...`(经 [[svc_sgs]] 网关 → [[svc_acquireii]] 收单核心) |
| 传输 / 提交 / 格式 | HTTPS / POST / JSON(UTF-8) |
| 鉴权 | 每次请求带 Header `sign`(商户私钥 **SHA256WithRSA** 签名)+ `Partner-Id`(商户号,≤12 字符);响应亦签名,需验签 |
| 语言 | Header `Content-Language`(可选,默认 English,≤10 字符) |
| 时效 | Body `requestTime` 与当前时间相差 >15 分钟被拒 |

签名 / 协议细节见 [[reference_acquire_protocol_and_codes]] 与场景 [[scn_online_business_openapi_protocol_signing]]。

## 公开接口目录(收单支付生命周期)
门户以 API 页组织,收单核心接口一一对应仓库内 `api_` 对象:

| 门户页 | 路径 | 仓库对象 |
| --- | --- | --- |
| Create Order | `/sgs/api/acquire2/placeOrder` | [[api_sgs_acquire_place_order]] |
| Retrieve Order Details (getOrder) | `/sgs/api/acquire2/getOrder` | [[api_sgs_acquire_get_order]] |
| Revoke Order | `/sgs/api/acquire2/revokeOrder` | [[api_sgs_acquire_revoke_order]] |
| Cancel Order | `/sgs/api/acquire2/cancelOrder` | [[api_sgs_acquire_cancel_order]] |
| Refund | `/sgs/api/acquire2/refund/placeOrder` | [[api_sgs_acquire_refund_place_order]] |

门户另含 **Integration Guide**、**Payment Overview**、**Transfer APIs**(转账到钱包等——属 wallet 域,非本域)与 **SDKs**(InApp SDK 等)。转账类对外接口归属钱包域,不在收单域展开。

## 与内部文档的差异(需以对外契约为准)
- **退款时效**:公开门户为**订单创建后 180 天内**可退;内部 v2.25 曾记为 100 天 → 已按门户更正 [[api_sgs_acquire_refund_place_order]]。
- **paySceneCode**:公开门户列出含 `PREAUTH` / `PREAUTHVOID` / `CAPTURE`(预授权/撤销/请款),已补入 [[reference_acquire_protocol_and_codes]]。
- **agreementInfo**(周期扣款/分期协议,DIRECTPAY):公开门户新增,已补入 [[api_sgs_acquire_place_order]]。

## QA 关注点
- **对外契约回归**:公开文档字段/错误码/时效变更 = 对外承诺变更,应触发对应 `api_` 对象核对与用例更新。
- **签名双向**:请求与响应都验签;`Partner-Id` ≤12、`requestTime` ±15 分钟是所有接口通用前置校验(任一接口都可作签名/时效负例)。
- **联调环境**:合作方用例跑 `uat.test2pay.com`;测试卡见 [[reference_cko_test_cards]] / [[reference_mpgs_test_cards]]。

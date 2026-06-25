---
id: api_ppc_card_activate
object_type: API
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: wiki:7dbfb622-f3fd-4ee5-b9cd-ba6eac0b5372
tags:
- card
- physical
- activate
subdomain: card-management
module: null
sensitivity: normal
name: 激活实体卡接口
aliases:
- Activate physical
- 激活实体卡
related_services:
- svc_ppc
---

## 用途
激活已配送到达的 PPC 实体卡，使其从 UNACTIVATED 状态转为可用状态。

## 路径/方法
- Method: POST
- Path（推断，待后端确认）: `/ppc/card/v1/activate`
- 调用方: App
- 网关: CGS (gp024_cgs)

## 入参
| 字段 | 说明 |
| --- | --- |
| `virtual_card_id` | 关联的虚拟卡 ID |
| `proxy_number` | 实体卡代理号 |

## 出参
原文未列出具体响应字段。参考 API 实时文档：https://sim-admin.corp.test2pay.com/api-doc/

## 错误码
| Code | 触发场景 |
| --- | --- |
| `INVALID_CARD_STATUS` | 卡状态非 UNACTIVATED（如已销卡 / 申请中 / Closing 中再次操作） |
| `VIRTUAL_CARD_NOT_EXIST` | 错误 ID 或异步消息延迟 |
| `PROCESSING_EXCEPTION` | 上下游异常（YSE/trade/grc） |
| `SYSTEM_EXCEPTION` | 兜底系统异常 |

## 测试校验点
- 卡状态前置校验：仅当 `virtual_card_id` 对应卡状态 = `UNACTIVATED` 时允许激活；其他状态必返回 `INVALID_CARD_STATUS`（反向状态用例必含）。
- 字段必填/边界：`virtual_card_id`、`proxy_number` 缺失或非法值。
- 串联用例（6-API 链路）：申请实体卡 → 支付 → 制卡 → 配送 → 激活；与 lock/unlock/close 形成完整生命周期。
- 幂等：重复激活同一卡应返回一致结果，DB 不产生重复激活记录。
- 上下游异常：YSE 处理异常返回 `PROCESSING_EXCEPTION`，需测试重试机制。
- 至少 1 条正向用例 + 每个声明错误码 1 条反向用例。

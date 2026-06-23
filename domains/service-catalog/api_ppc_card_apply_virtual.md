---
id: api_ppc_card_apply_virtual
object_type: API
domain: service-catalog
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: wiki:7dbfb622-f3fd-4ee5-b9cd-ba6eac0b5372
tags:
- card-management
- virtual-card
- MC
- PR
subdomain: card-management
module: null
sensitivity: normal
name: 申请虚拟卡接口
aliases:
- Apply virtual card
related_services:
- svc_ppc
---

## 用途
App 端用户申请 PPC 虚拟卡（MC / PR 类型），完成 KYC 校验后创建虚拟卡记录。

## 路径/方法
- Method: `POST`
- Path（推断，待后端确认）: `/ppc/card/v1/apply-virtual`
- 网关: CGS (`gp024_cgs`)
- 调用方: App

## 入参
| 字段 | 说明 |
|---|---|
| `member_id` | 会员 ID |
| `card_type` | 卡类型，枚举 MC / PR |
| `kyc_token` | KYC 校验通过 token |

幂等键: `member_id + card_type + session_id`

## 出参
原文未明确列出，参见在线 API 文档 https://sim-admin.corp.test2pay.com/api-doc/

## 错误码
| Code | 触发场景 |
|---|---|
| `KYC_NOT_VERIFIED` | KYC 未通过，申请卡前置校验失败 |
| `VIRTUAL_CARD_TYPE_NOT_EXIST` | 卡类型 (MC/PR) 未配置 / BIN 路由异常 |
| `PROCESSING_EXCEPTION` | 上下游处理异常（YSE/trade/grc） |
| `SYSTEM_EXCEPTION` | 系统兜底异常 |

## 测试校验点
- 正向：合法 `member_id` + `card_type=MC`/`PR` + 有效 `kyc_token` → 创建虚拟卡成功。
- 反向错误码：每个声明错误码至少 1 条用例。
  - KYC 未通过 → `KYC_NOT_VERIFIED`
  - 非法 / 未配置卡类型 → `VIRTUAL_CARD_TYPE_NOT_EXIST`
  - 下游异常 → `PROCESSING_EXCEPTION`，验证重试机制
  - 系统兜底 → `SYSTEM_EXCEPTION`，必测降级
- 字段边界：`card_type` 仅允许 MC / PR；非法值需拒绝；`kyc_token` 失效/过期需拒绝。
- 幂等性：相同 `member_id + card_type + session_id` 重复请求 → 返回相同结果，DB 不创建新记录。
- 串联用例：作为 5-API 链路起点（申请 → 激活 → 锁 → 解锁 → 关闭）的首步。
- 核身依赖：本接口依赖 `kyc_token`，失效 token 必拒。

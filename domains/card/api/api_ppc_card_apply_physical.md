---
id: api_ppc_card_apply_physical
object_type: API
domain: card
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: wiki:7dbfb622-f3fd-4ee5-b9cd-ba6eac0b5372
tags:
- card
- physical
- apply
- delivery
subdomain: card-management
module: null
sensitivity: normal
name: 申请实体卡接口
aliases:
- Apply physical card
- init-apply-physical
- apply-physical
related_services:
- svc_ppc
---

## 用途
提交实体卡申请，含初始化（拉取默认收件信息）与正式提交（含收件信息与卡样式）两步。提交时会关闭未支付的旧订单。属于实体卡 6-API 串联链路（physical-apply→pay→produce→ship→activate）的首环。

## 路径/方法
- 初始化 / Init apply physical: `POST /ppc/card/v1/init-apply-physical` （路径为推断，待后端确认）
- 提交 / Apply physical with delivery: `POST /ppc/card/v1/apply-physical` （路径为推断，待后端确认）
- 网关：CGS（gp024_cgs），调用方：App

## 入参
### init-apply-physical
- `virtual_card_id`：所属虚拟卡 ID
- 返回：默认 `delivery_address` + 默认 `card_holder_name`

### apply-physical
- `virtual_card_id`：所属虚拟卡 ID
- `card_holder_name`：持卡人姓名，长度 ≤ 25
- `delivery_address`：收件地址
- `card_style`：卡样式，枚举 `Standard` / `Metal`

## 出参
原文未列出响应字段。提交成功后生成实体卡订单（用于后续支付与 `tracking-physical-card-order` 跟踪，关联 `order_id`）。

## 错误码
适用通用错误码：
- `INVALID_CARD_STATUS`：虚拟卡状态不允许申请实体卡
- `VIRTUAL_CARD_NOT_EXIST`：传入的 `virtual_card_id` 不存在
- `VIRTUAL_CARD_TYPE_NOT_EXIST`：卡类型未配置 / BIN 路由异常
- `KYC_NOT_VERIFIED`：KYC 未通过（申请卡前置校验）
- `PROCESSING_EXCEPTION`：上下游异常（YSE/trade/grc）
- `SYSTEM_EXCEPTION`：兜底系统异常

## 测试校验点
- 正向：init 返回默认地址/姓名 → 提交成功生成订单。
- 字段边界：
  - `card_holder_name` = 25 字符（边界）/ > 25（拒绝）/ 特殊字符
  - `card_style` 仅接受 `Standard` / `Metal`，非法值拒绝
  - `delivery_address` 必填校验
- 反向：
  - `virtual_card_id` 不存在 → `VIRTUAL_CARD_NOT_EXIST`
  - 虚拟卡处于不允许状态（如 Closing/已销卡）→ `INVALID_CARD_STATUS`
  - KYC 未通过 → `KYC_NOT_VERIFIED`
- 业务规则：
  - 提交时若存在未支付旧订单，应被关闭（验证旧订单状态翻转，不产生重复未支付订单）
- 串联用例：
  - 6-API 链路：申请实体卡 → 支付 → 制卡（trade notify 推 YSE）→ 配送（USP/Jeebly）→ 激活（[[api_ppc_card_activate]]）
- 异步时序：实体卡支付完成走 `/ppc/trade/notify`，需保证 apply 与 trade notify 的幂等与对账。

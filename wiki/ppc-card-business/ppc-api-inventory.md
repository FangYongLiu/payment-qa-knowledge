---
title: PPC核心API清单
domain: ppc-card-business
kind: wiki_page
slug: ppc-api-inventory
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:7dbfb622-f3fd-4ee5-b9cd-ba6eac0b5372
tags: []
---

# PPC核心API清单

PPC 系统对外/内部 API 全景清单，覆盖网关、卡管理、交易/账务、卡组织出入向回调，以及供 AI 推导接口/集成测试用例的提示。

## API 网关

| 网关 | 用途 | App / 服务 |
|---|---|---|
| CGS (Client Gateway Service) | App / Web / H5 调用 | gp024_cgs |
| SGS (Server Gateway Service) | 内部服务 / 商户调用 | gp028_sgs |
| API doc | Smart-doc 自动生成接口文档 | https://sim-admin.corp.test2pay.com/api-doc/ |

> Path 列均为推断格式，待后端确认。

## 卡管理 API

按业务流程分组，所有路径前缀 `/ppc/card/v1/`，调用方为 App。

### 概览与查询

| 操作 | Method | Path | 关键字段 |
|---|---|---|---|
| 获取卡概览 | GET | `/summary` | `member_id` |
| 查看卡明细 | GET | `/detail` | `virtual_card_id`, `identity_verify_token` |
| 查看卡号 (PAN) | GET | `/pan` | `virtual_card_id`, `identity_verify_token`（YSE 查询接口） |

### 申请与 PIN

- [[api_ppc_card_apply_virtual]] `POST /apply-virtual` — 字段 `member_id`, `card_type` (MC/PR), `kyc_token`；幂等键 `member_id + card_type + session_id`
- [[api_ppc_card_set_pin]] `POST /set-pin` — 字段 `virtual_card_id`, `pin` (encrypted), `confirm_pin`, `identity_verify_token`
- [[api_ppc_card_reset_pin]] `POST /reset-pin` — 字段 `virtual_card_id`, `pin`, `identity_verify_token`；调 APIPTR 解锁 PIN

### 卡状态变更

- [[api_ppc_card_lock]] `POST /lock` — 幂等键 `virtual_card_id + operate_session_id`（弱网防重复, BUG-6548）
- [[api_ppc_card_unlock]] `POST /unlock` — 同上幂等键（BUG-6554）
- [[api_ppc_card_replace]] `POST /replace` — 累计 ≤ 3 次
- [[api_ppc_card_close]] `POST /close` — 字段含 `close_reason`；幂等键 `virtual_card_id + close_session_id`

### 实体卡

- `POST /init-apply-physical` — 入参 `virtual_card_id`，返回默认地址 + 名称
- [[api_ppc_card_apply_physical]] `POST /apply-physical` — 字段 `card_holder_name` (≤25), `delivery_address`, `card_style` (Standard/Metal)；关闭未支付旧订单
- [[api_ppc_card_track_physical]] `GET /tracking-physical-card-order` — 入参 `order_id`；字段 `mobilePhoneNumber` (BUG-6892), `fees` (BUG-6893)
- [[api_ppc_card_activate]] `POST /activate` — 字段 `virtual_card_id`, `proxy_number`；卡状态校验 = `UNACTIVATED`

## 交易/账务 API

| 操作 | Method | Path | 备注 |
|---|---|---|---|
| 查询交易明细 | GET | `/ppc/card/v1/transactions` | |
| 充值 (add funds) | POST | `/ppc/card/v1/add-funds` | |
| 货币转换 | POST | `/ppc/fx/v1/convert` | |
| 汇率试算 | POST | `/ppc/fx/v1/calculate` | 弱网键盘关闭后不应调用 (BUG-6529) |
| 下载交易单 | GET | `/ppc/card/v1/statement` | App / H5 |

## 卡组织接口（出向 YSE / Jaywan）

详见 `卡组织接口` / `ppc-SD-Processor API` 页。重要接口：

- **Authorization (APIAUT)** — 授权报文；`ResponseCode=75` 表示 PIN locked
- **PIN Tries Reset (APIPTR)** — 解锁 PIN
- **Card Status Update** — 卡状态变更通知（入向）
- **Update Card Detail** — YSE 卡信息更新通知（入向）

## 卡组织回调（入向）

| 事件 | Method | Path | 触发方 | 处理动作 |
|---|---|---|---|---|
| Authorization | POST | `/ppc/yse/notify/auth` ([[api_ppc_yse_auth_notify]]) | YSE/Jaywan | 校验余额、写授权流水、设置 Pending Account |
| Clearing / Settle | POST | `/ppc/yse/notify/clearing` ([[api_ppc_yse_clearing_notify]]) | YSE/Jaywan | Pending → Settle / Refund / Reversal |
| PIN Locked | POST | `/ppc/yse/notify/pin-lock` | YSE | 标记 PIN locked |
| Card Detail Update | POST | `/ppc/yse/notify/card-update` | YSE | 同步本地卡数据 |
| Trade Notify | POST | `/ppc/trade/notify` | trade 服务 | 实体卡支付完成 → 推 YSE 制卡 / 关卡 |
| Shipment Notify | POST | `/ppc/usp/notify/shipment` | USP/Jeebly | 配送状态变更 |
| Biometrics Notify | POST | `/ppc/usp/notify/biometrics` | USP | 生物信息上传 |
| Jeebly Delivery Status | POST | `/ppc/api/jeebly/delivery-status` ([[api_ppc_jeebly_delivery_status]]) | Jeebly | 状态：Out for delivery / Delivered / Cancelled / RTO Delivered（BUG-8948 RTO 处理报错） |

## 测试用例生成提示

- **API 覆盖度**：每个 API 至少 1 条正向用例；返回的每个错误码至少 1 条反向用例。
- **字段边界**：金额（精度/边界/负数）、字符串（长度边界、特殊字符）、币种（合法/非法 ISO）、PAN/CVV（必加密）。
- **幂等性**：每个标注幂等键的 API 必出 1 条重复请求用例 → 返回相同结果，DB 不创建新记录。
- **串联用例**：
  - 5-API 链路：申请 → 激活 → 锁 → 解锁 → 关闭
  - 6-API 链路：申请实体卡 → 支付 → 制卡 → 配送 → 激活
- **回调时序**：异步 callback 乱序、重投、丢失、超时 → 必测幂等 + 兜底对账。
- **核身依赖**：所有需 `identity_verify_token` 的 API → 失效 token 必拒。
- **总估算**：30+ APIs × 平均 4 条（happy + 错误码 + 边界 + 幂等）= **~120 条** API 层用例。

错误码细节与反向用例提示见 [[ppc-common-error-codes]]。

## 外部参考

- `

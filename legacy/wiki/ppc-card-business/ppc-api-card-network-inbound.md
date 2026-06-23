---
title: PPC卡组织回调（入向）API清单
domain: ppc-card-business
kind: wiki_page
slug: ppc-api-card-network-inbound
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2133098640
tags: []
---

# PPC卡组织回调（入向）API清单

本页梳理 PPC 系统从卡组织（YSE/Jaywan）、配送商（USP/Jeebly）、内部 trade 服务接收的入向回调事件清单，用于 AI 推导异步回调相关的测试用例（幂等、乱序、重投、对账兜底等）。

## 范围与边界

- 本页仅列**入向**回调（Card Network / 配送 / Trade → PPC）。
- 出向调用（PPC → YSE/Jaywan，如 Authorization 请求、APIPTR 解锁 PIN、Card Status Update 通知等）见 [[ppc-api-inventory-overview]] 中"卡组织接口（出向）"部分。
- Path 为推断格式，最终以后端确认为准。

## 回调事件清单

| 事件 / Event | Method | Path（推断） | 触发方 | 处理动作 |
|---|---|---|---|---|
| Authorization | POST | `/ppc/yse/notify/auth` | YSE/Jaywan | 校验余额、写入授权流水、设置 Pending Account |
| Clearing / Settle | POST | `/ppc/yse/notify/clearing` | YSE/Jaywan | Pending → Settle / Refund / Reversal |
| PIN Locked | POST | `/ppc/yse/notify/pin-lock` | YSE | 标记 PIN locked |
| Card Detail Update | POST | `/ppc/yse/notify/card-update` | YSE | 同步本地卡数据 |
| Trade Notify | POST | `/ppc/trade/notify` | trade 服务 | 实体卡支付完成 → 推 YSE 制卡 / 关卡 |
| Shipment Notify | POST | `/ppc/usp/notify/shipment` | USP/Jeebly | 配送状态变更 |
| Biometrics Notify | POST | `/ppc/usp/notify/biometrics` | USP | 生物信息上传 |
| Jeebly Delivery Status | POST | `/ppc/api/jeebly/delivery-status` | Jeebly | 状态：Out for delivery / Delivered / Cancelled / RTO Delivered |

## 关键事件说明

### Authorization（YSE/Jaywan）
- 授权报文入向，PPC 校验余额并落授权流水。
- 创建 **Pending Account** 占用余额。
- 与出向 APIAUT 报文配对；`ResponseCode=75` 表示 PIN locked。

### Clearing / Settle
- Pending Account 推进到最终状态：**Settle / Refund / Reversal**。
- 账务影响详见外部文档 `ppc-SD-3-Transaction`。

### PIN Locked
- 用户 PIN 连续错误达上限，YSE 通知后本地标记 PIN locked。
- 解锁需走出向 APIPTR（PIN Tries Reset）。

### Trade Notify
- 实体卡用户支付完成后，trade 服务回调 PPC。
- PPC 据此向 YSE 推送制卡或关卡指令。

### Jeebly Delivery Status
- 状态枚举：`Out for delivery` / `Delivered` / `Cancelled` / `RTO Delivered`。
- 已知问题：BUG-8948 — RTO Delivered 处理报错。

## 已知缺陷

- **BUG-8948**：Jeebly `RTO Delivered` 状态回调处理报错。

## 测试用例生成提示

回调类 API 的核心测试维度：

- **幂等性**：同一回调重投（相同业务单号）→ 不重复入账、状态不回退。
- **乱序**：Clearing 早于 Authorization 到达 → 必须能通过对账兜底正确处理。
- **重投 / 丢失 / 超时**：依赖异步重试机制，必测幂等 + 对账兜底。
- **状态机**：Pending → Settle / Refund / Reversal 的非法跃迁必拒。
- **Jeebly 状态枚举**：四种状态各 1 条正向用例 + RTO 异常路径回归（BUG-8948）。
- **签名/来源校验**：非法来源、签名错误必拒。

相关错误码（`PROCESSING_EXCEPTION`、`SYSTEM_EXCEPTION`、`VIRTUAL_CARD_NOT_EXIST` 等）见 [[ppc-api-error-codes]]，通用生成方法论见 [[ppc-api-test-case-generation-hints]]。

## 关联页面

- 出向卡组织调用与卡状态联动 → [[ppc-api-card-management]]
- 入向回调对应的账务流水 → [[ppc-api-transaction]]
- 网关与路由 → [[ppc-api-gateways]]

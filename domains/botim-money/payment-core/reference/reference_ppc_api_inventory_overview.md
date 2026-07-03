---
id: reference_ppc_api_inventory_overview
object_type: Reference
name: PPC核心API清单总览
aliases: [ppc-api-inventory-overview]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
source_type: wiki
source_ref: confluence:AQ/2133098640
tags: [payment-core, wiki-overview]
related_services: [svc_cgs, svc_ppc]
related_tables: []
---


# PPC核心API清单总览

PPC 系统 API 知识库总入口，覆盖 API 网关、按业务分组的接口清单、通用错误码以及 AI 测试用例生成提示，供接口/集成测试用例推导使用。

## 用途

- 列出 PPC 对外/内部 API 的完整清单
- 作为 AI 生成测试用例的事实来源：API 覆盖、字段边界、错误码反向、幂等、跨 API 串联
- 接口 PR 变更时同步更新本页
- 维护人：Jianfei Wang；后端 reviewer：Yu Tang / Xiaoyu Sun
- 状态：部分填充，endpoint 路径待后端确认

## 子页导航

- ppc-api-gateways — CGS / SGS 网关与 API doc 入口
- [[ppc-api-card-management]] — 卡管理 API（申请、PIN、查看、锁/解锁、替换、关闭、实体卡申请/激活/跟踪）
- [[ppc-api-transaction]] — 交易/账务 API（明细、充值、FX、对账单）
- ppc-api-card-network-inbound — 卡组织及外部回调入向 API（YSE / trade / USP / Jeebly）
- [[ppc-api-error-codes]] — 通用错误码与触发场景
- ppc-api-test-case-generation-hints — 测试用例生成指引（覆盖、边界、幂等、串联、异步时序）

## 出向卡组织接口

PPC 出向调用 YSE / Jaywan 接口，详见独立的 Card Network Interface 文档（不在本知识库展开）。关键接口：

- `Authorization` (APIAUT) — 授权报文，`ResponseCode=75` 表示 PIN locked
- `PIN Tries Reset` (APIPTR) — 解锁 PIN
- `Card Status Update` — 卡状态变更通知（入向）
- `Update Card Detail` — YSE 卡信息更新通知（入向）

入向回调（YSE Authorization / Clearing / PIN Locked / Card Detail Update / trade / USP / Jeebly）请查阅 ppc-api-card-network-inbound。

## 总用例估算

- 30+ APIs × 平均 4 条用例（happy + 错误码 + 边界 + 幂等）≈ **~120 条 API 层用例**
- 生成方法详见 ppc-api-test-case-generation-hints

## 外部参考

- `ppc-SD-3-Transaction` — Authorization / Clearing / Reversal 账务细节
- `ppc-OP-3-Fee Config` — 交易类型枚举（T/S/R/RL/F/CB/RF/FRL）
- `ppc-2-流程图设计` — 各流程服务交互图
- `ppc-SD-Processor API` — 卡组织接口源
- API 文档（Smart-doc 实时）：`https://sim-admin.corp.test2pay.com/api-doc/`

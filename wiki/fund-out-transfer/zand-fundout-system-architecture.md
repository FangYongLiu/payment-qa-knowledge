---
title: ZAND Fundout系统架构与API调用链
domain: fund-out-transfer
kind: wiki_page
slug: zand-fundout-system-architecture
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:7f334321-3b49-4c87-b6d9-8949925a962a
tags: []
---

# ZAND Fundout系统架构与API调用链

本页聚焦 ZAND Fundout 的系统分层、服务职责、API 调用链路与重试策略。业务背景与渠道映射见 [[zand-fundout-overview]]，端到端流程见 [[flow_zand_fundout]]。

## 系统分层与服务职责

| 服务/组件 | 职责 | 数据库 |
|---|---|---|
| SGS API Gateway | 鉴权、参数校验、限流 | - |
| Fundout Service | 订单创建、收款人校验、FX | mhtfundout |
| Kafka MQ | 异步消息(`fundout.created` / `processing` / `status.update`) | - |
| CMF Router | 渠道路由、渠道指令订单管理 | cmf |
| ZAND Bank APIs | 提供 SP / SQ / VS 接口 | - |
| FCW Webhook Receiver | HMAC 校验、回写 CMF 状态 | - |
| DPM Accounting | 余额、手续费、台账 | dpm |

## 架构调用层次

```
Client (Merchant Portal | Botim App | Partner API)
   ↓
SGS API Gateway
   ↓
Fundout Service  (t_fundout_order / t_fundout_beneficiary / t_fundout_bankcard_order)
   ↓ Kafka
CMF Router       (tt_inst_order / tt_inst_order_result; ZAND201/203/204/207/210)
   ↓
ZAND Bank APIs (SP / SQ / VS)
   ↓ VS
FCW Webhook Receiver  →  CMF 更新  →  DPM 记账
```

相关存储：[[tbl_mhtfundout_t_fundout_order]]、[[tbl_mhtfundout_t_fundout_bankcard_order]]、[[tbl_cmf_tt_inst_order]]、[[tbl_cmf_tt_inst_order_result]]、[[tbl_router_t_channel_result_code]]。

## API 调用链

### 国内转账 (ZAND201)

1. Client → SGS Gateway → Fundout Service 创建订单
2. Fundout Service → Kafka → CMF Router 路由到 ZAND201
3. CMF → ZAND Bank **SP** API 提交付款，返回 ChannelRefId（`D...`）
4. ZAND Bank → FCW Webhook **VS** 回调（`COMPLETED`）
5. FCW → CMF 更新状态为 `S` → DPM 扣减余额

### 国际 SWIFT 转账 (ZAND203)

1. Client → SGS Gateway → Fundout Service 创建订单
2. Fundout Service → Kafka → CMF Router 路由到 ZAND203
3. CMF → ZAND Bank **SP** API 提交付款，返回 ChannelRefId（`ZIT...`）
4. CMF → ZAND Bank **SQ** API 周期性轮询
5. ZAND Bank → FCW Webhook **VS** 回调（`PROCESSED`）
6. FCW → CMF 更新状态为 `S` → DPM 扣减余额并计费

## SP / SQ / VS 三类指令

| 类型 | 含义 | 说明 |
|---|---|---|
| SP | Submit Payment | 系统向 ZAND 发起付款，返回 ChannelRefId |
| SQ | Status Query | 系统轮询 ZAND 查询状态（仅国际） |
| VS | Vendor Status | ZAND Webhook 回调最终状态（COMPLETED / PROCESSED） |

- 国内：`SP → VS`（约 12 秒，无需 SQ）
- 国际：`SP → SQ（轮询）→ VS`

## 重试机制

### SP 失败/超时
- 进入重试处理器，使用指数退避（exponential backoff）
- 写入重试队列，由 worker 重新提交
- 成功则更新订单；永久失败则回退手续费

### SQ 轮询节奏
- SP 后约前 2 分钟较密集
- 间隔逐步加大
- `RETRY_TIMES > 35` 时间隔进入小时级
- `RETRY_TIMES = 54` 停止轮询

## 关键状态码

| 库.表 | 字段 | 取值 |
|---|---|---|
| mhtfundout.t_fundout_order | status | CREATED / PLACED / SUCCESS / FAILURE |
| cmf.tt_inst_order | STATUS | I（处理中）/ S（成功）/ F（失败）/ U（未知） |
| cmf.tt_inst_order_result | API_TYPE | SP / SQ / VS |

渠道返回码到 CMF 状态的映射由 [[tbl_router_t_channel_result_code]] 控制（如 `PROCESSED → result_status=S`）。

## 关联页面

- 测试方法与校验 SQL：[[zand-fundout-test-guide]]
- 故障排查（路由失败、VS 不到达、签名错误等）：[[zand-fundout-troubleshooting]]
- 用例集合：[[scn_zand_fundout_test_cases]]
- Mock VS 工具：[[auto_zand_mock_vs_tool]]

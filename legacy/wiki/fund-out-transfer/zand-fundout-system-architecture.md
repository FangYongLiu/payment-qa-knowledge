---
title: ZAND Fundout系统架构与调用链
domain: fund-out-transfer
kind: wiki_page
slug: zand-fundout-system-architecture
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2049867832
tags: []
---

# ZAND Fundout系统架构与调用链

本页聚焦 ZAND 出款链路的系统组成、SP/SQ/VS 调用编排、重试与轮询机制，以及落库的关键表与状态。业务背景与渠道清单见 [[zand-fundout-overview]]。

## 系统架构分层

| 服务/组件 | 职责 | 数据库 |
|---|---|---|
| SGS API Gateway | Auth、Validation、Rate Limiting | - |
| Fundout Service | 订单创建、收款人校验、FX | mhtfundout |
| Kafka MQ | 异步消息：fundout.created / processing / status.update | - |
| CMF Router | 渠道路由、订单管理 | cmf |
| ZAND Bank APIs | SP / SQ / VS 端点 | - |
| FCW Webhook Receiver | HMAC 验签，依据 VS 回写 CMF | - |
| DPM Accounting | 余额、手续费、台账 | dpm |

入口包括 Merchant Portal、Botim App、Partner API。

## 调用链：Domestic Transfer (ZAND201)

1. Client -> SGS Gateway -> Fundout Service（创建订单）
2. Fundout Service -> Kafka -> CMF Router（路由到 ZAND201）
3. CMF -> ZAND Bank SP API（提交支付，返回 ChannelRefId，前缀 `D`）
4. ZAND Bank -> FCW Webhook（VS 回调，COMPLETED）
5. FCW -> CMF（更新 STATUS=S）-> DPM（扣减余额）

特点：SP -> VS，无需 SQ 轮询，约 12 秒完成。

## 调用链：International Transfer (ZAND203)

1. Client -> SGS Gateway -> Fundout Service（创建订单）
2. Fundout Service -> Kafka -> CMF Router（路由到 ZAND203）
3. CMF -> ZAND Bank SP API（提交支付，返回 ChannelRefId，前缀 `ZIT`）
4. CMF -> ZAND Bank SQ API（按间隔轮询）
5. ZAND Bank -> FCW Webhook（VS 回调，PROCESSED）
6. FCW -> CMF（更新 STATUS=S）-> DPM（扣余额、计费）

端到端流程图见 [[flow_zand_fundout]]。

## 重试与轮询机制

### SP 失败/超时重试
- 进入 retry handler，采用指数退避（exponential backoff）
- 写入重试队列，由 worker 重新提交
- 成功 -> 更新订单；永久失败 -> 反向冲销手续费

### SQ 轮询策略
- SP 后约前 2 分钟为初始轮询窗口
- 间隔随时间逐步增大
- `RETRY_TIMES > 35`：间隔扩大到小时级
- `RETRY_TIMES = 54`：停止轮询

## 关键数据库表

| 表 | 库 | 用途 | 关键字段 |
|---|---|---|---|
| t_fundout_order | mhtfundout | Fundout 主订单 | global_id, partner_id, status, product_code |
| t_fundout_bankcard_order | mhtfundout | 银行卡订单明细 | fundout_crcy_code, fundout_amount, network_code, rate |
| tt_inst_order | cmf | CMF 渠道订单 | INST_ORDER_NO, FUND_CHANNEL_CODE, STATUS, AMOUNT, RETRY_TIMES |
| tt_inst_order_result | cmf | SP/SQ/VS 结果 | API_TYPE, INST_STATUS, INST_SEQ_NO, EXTENSION, MEMO |
| t_channel_result_code | router | 银行响应码 -> CMF 状态映射 | channel_code, api_type, result_code, result_sub_code, result_status |
| t_dpm_outer_account_subset | dpm | 账户余额 | BALANCE, CURRENCY |
| t_settlement_detail | reconciliation | 结算记录 | settlement_status, settlement_amount, settlement_currency |

详见 [[tbl_mhtfundout_t_fundout_order]]、[[tbl_mhtfundout_t_fundout_bankcard_order]]、[[tbl_cmf_tt_inst_order]]、[[tbl_cmf_tt_inst_order_result]]。

## 状态码

| 库.表 | 字段 | 取值 |
|---|---|---|
| mhtfundout.t_fundout_order | status | CREATED, PLACED, SUCCESS, FAILURE |
| cmf.tt_inst_order | STATUS | I (In Process), S (Success), F (Failed), U (Unknown) |
| cmf.tt_inst_order_result | API_TYPE | SP, SQ, VS |

## SP/SQ/VS 落库校验要点

| 步骤 | 校验内容 |
|---|---|
| SP | INST_STATUS=I；INST_SEQ_NO 为 `D...` 或 `ZIT...`；EXTENSION 含 CreationDateTime、ChannelRefId、channelTransTime |
| SQ（仅国际） | INST_STATUS=I 或 S；ChannelRefId 与 SP 一致；EXTENSION 同 SP |
| VS（domestic） | INST_STATUS=S；MEMO=`Credited To Beneficiary`；Type=`OUTGOING_DOMESTIC_TRANSACTION_STATUS` |
| VS（international） | INST_STATUS=S；MEMO=`PROCESSED`；Type=`OUTGOING_INTERNATIONAL_TRANSACTION_STATUS` |

## 相关页面

- 测试方法与 Mock VS 操作：[[zand-fundout-testing-guide]]
- 排障与常见错误：[[zand-fundout-troubleshooting]]

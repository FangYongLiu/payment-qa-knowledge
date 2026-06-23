---
id: tbl_mhtfundout_t_fundout_bankcard_order
object_type: Table
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:AQ/2049867832
tags:
- mhtfundout
- bankcard
- fundout
subdomain: null
module: null
sensitivity: normal
name: Fundout银行卡订单表 t_fundout_bankcard_order
aliases: []
related_services:
- svc_fundout
---

## 用途
位于 `mhtfundout` 库，存储 Fundout 出款订单的银行卡(收款方银行账户)维度详情，记录出款币种、金额、网络、汇率等信息，与主表 `t_fundout_order` 配套使用，支撑 Fundout Service 在下单时进行受益人校验、币种与汇率处理。

## 关键列
- `fundout_crcy_code`：出款币种(如 AED / USD)
- `fundout_amount`：出款金额
- `network_code`：使用的网络/通道标识(对应 ZAND201/203/204/207/210 等场景)
- `rate`：汇率(国际转账涉及外币换算时使用)

## 主键/索引
原文未提供主键/索引定义。

## 校验点(QA 关注)
- 域内转账(IBAN 以 AE 开头, ZAND201/210)：`fundout_crcy_code` 应为 AED；金额与主表 `t_fundout_order` 一致。
- 国际 SWIFT(ZAND203/207)：`fundout_crcy_code` 为 USD，`rate` 应填入对应汇率，金额与最终扣款/费用(如 157.50 AED)可核对。
- `network_code` 应与 CMF `tt_inst_order.FUND_CHANNEL_CODE` 选定的渠道对应(ZAND201 / ZAND203 / ZAND204 / ZAND207 / ZAND210)。
- 与主表关联：`t_fundout_order.global_id`(18 位 Fundout Order ID，如 131773657853407506) 应能关联到本表银行卡订单详情。
- 异常情况：若主表 `unity_result_code = cmf.route.fail`，需结合本表的 `network_code` 与路由配置确认是否路由错误(例如错路由到 TEST201 而非 ZAND203)。
- 原文未提及本表直接存储 ChannelRefId(D.../ZIT...)，该字段位于 CMF 结果表 `tt_inst_order_result.INST_SEQ_NO`，避免越界校验。

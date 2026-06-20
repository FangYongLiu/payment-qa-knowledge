---
title: Life-Center SGS 手机充值下单流程
domain: payby-open-api
kind: wiki_page
slug: life-center-sgs-mobile-recharge-flow
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:9250fa4b-3c03-44a7-ba60-f532ee44a868
tags: []
---

# Life-Center SGS 手机充值下单流程

本页描述 partner 通过 SGS 网关调用 life-center 完成手机充值下单的调用链路，包括同步下单与异步 MQ 结果通知两段流程。

## 参与方

- **partner**：外部商户/调用方
- **sgs**：开放网关
- **life-center**：业务编排层
- **market-goods**：商品服务
- **market-order**：订单服务
- **transfer**：转账/资金处理服务
- **cps**：风控/限额服务
- **pns**：通知服务

## 同步下单链路

入口接口：`/lifecenter/goods/v1/place-mobile-order`

调用顺序：

1. `partner → sgs`：调用 `/lifecenter/goods/v1/place-mobile-order`
2. `sgs → life-center`：转发请求
3. `life-center → market-goods`：`GoodsFacade#detail` 查询商品详情
4. `life-center → market-order`：`OrderCreateFacade#createOrder` 创建订单
   - `market-order → cps`：`LimitQuotaFrequencyStub#mobileRechargeLimitQuotaAndTimes` 校验手机充值限额与频次
   - `market-order → transfer`：`TransferOrderFacade#transferIntermediary` 发起中间账户转账
   - `market-order → life-center`：返回创建结果
5. 同步响应沿 `life-center → sgs → partner` 逐级返回

## 异步结果通知链路

资金侧处理完成后，通过 MQ 逐级回传至商户：

1. `transfer`：`process result` 处理转账结果（自调用）
2. `transfer → market-order`：`process mq` 推送结果消息
3. `market-order → life-center`：`process mq` 转发消息
4. `life-center → pns`：`GeneralNotifyFacade#notifyMerchant` 通知商户

## 关键点

- 同步链路完成订单创建与资金动作发起，不等待最终结果
- 限额/频次校验在 `market-order` 内完成，依赖 `cps`
- 商户最终结果通过 MQ 异步驱动，由 `pns` 统一对外通知

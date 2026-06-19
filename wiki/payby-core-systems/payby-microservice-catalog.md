---
title: PayBy 微服务全景清单
domain: payby-core-systems
kind: wiki_page
slug: payby-microservice-catalog
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:2bc88b9d-fdd4-46f9-a4aa-7ef0774c7418
tags: []
---

# PayBy 微服务全景清单

本页汇总 PayBy 平台所有微服务（含活跃与已废弃），按业务分类列出系统编号、缩写、中英文名称、职责说明与负责人，作为服务地图的总目录。活跃子集见 [[payby-active-microservices]]，分类拓扑见 [[payby-service-category-map]]。

## 01 - 网关

| 编号 | 缩写 | 名称 | 说明 | 负责人 |
|---|---|---|---|---|
| gp024_cgs | cgs | Client Gateway Service / 客户端网关 | 对 SDK / H5 暴露 HTTP API，按配置路由到业务服务，含验签、加解密转换、限流等。接收用户浏览器和手机应用请求 | 喻赛 |
| - | sgs | Server Gateway / 服务端网关 | 接收商户后台服务器请求 | 喻赛 |
| gp013_pns | pns | Partner Notify Service / 商户通知服务 | 商户通知服务 | 喻赛 |

## 02 - 应用

| 编号 | 缩写 | 名称 | 说明 | 负责人 |
|---|---|---|---|---|
| gp032_personal | personal | 个人应用 Personal | 提供 wallet 服务：充值、提现等 | 喻赛 |
| gp053_transfer | transfer | 转账服务 | 提供 wallet transfer、split bill、red packet 等转账能力，调用 trade 完成交易 | 刘智斌 |
| gp035_socialpay | socialpay | 社交支付应用 Social Pay | 红包、AA 收款等，调用 transfer（开发中） | 刘智斌 |
| gp007_cashdesk-api | cashdesk-api | 收银台接口（旧） | 旧版收银台，多数功能已被 cashierii 取代，不含 cashier withdraw 流程 | 高一春 |
| gp193_cashierii | cashierii | 收银台 | 面向 app / paypage / pos 的 checkout API，含风险识别、商户鉴权与支付流程 | - |
| gp027_paycode-pcm | pcm | PayCode Manager / 付款码应用 | 付款码管理：上传密钥、刷新、查询等 | 高一春 |
| gp076_market-order | market-order | 公共事业缴费-订单系统 | market order | 喻赛 |
| gp075_market-goods | market-goods | 公共事业缴费-商品系统 | market goods | 喻赛 |
| gp074_life-center | life-center | 公共事业缴费-前置 Life Center | - | 喻赛 |
| gp098_green-points | green-points | 积分应用 | 各承运商积分对接平台，积分发行销毁入口 | 喻赛 |
| - | - | Acquire Service / 收单服务 | - | 沈阅 |

## 03 - 支付中台

| 编号 | 缩写 | 名称 | 说明 | 负责人 |
|---|---|---|---|---|
| gp123_tradeii | tradeii | API Integration / 交易 II | 提供基础 trade API，支持需要/不需要 checkout 的支付场景 | - |
| gp010_trade | trade | 交易服务 | - | 唐宇 |
| gp011_deposit | deposit | 存款/充值服务 | 为 wallet、vis、kiosk 提供基础 top-up API，同时承担充值业务服务 | 唐宇 |
| gp012_fundout | fundout | 出款/提现服务 | 为 wallet 与商户提供基础 fundout API，同时承担提现业务服务 | 唐宇 |
| gp014_pfs-payment | pfs-payment | 支付前置-支付服务 | 定义可扩展业务支付 API，存储支付基础信息，对业务支付单进行校验、增强与持久化，按订阅发送统一支付结果消息 | 李德文 |
| gp014_pfs-basis | pfs-basis | 支付前置-对外基础服务 | - | 李德文 |
| gp014_pfs-manager | pfs-manager | 支付前置-后台管理服务 | - | 李德文 |
| gp006_payment | payment | 支付引擎 | 根据支付服务定义与参与方清结算协议控制支付指令处理流程，对成功指令做债权债务清分与资金划拨；提供清算规则配置 | 李德文 |
| gp004_dpm-accounting | dpm-accounting | 储值-记账 | 账户与科目管理、复式记账、缓冲记账；提供基于账户属性的三种入账规则及配套查询接口 | 周聪 |
| gp004_dpm-task | dpm-task | 储值-批量任务 | 储值批处理，主要处理缓冲入账 | 周聪 |
| gp004_dpm-manager | dpm-manager | 储值-管理接口 | 开户、查询等账户管理服务 | 周聪 |

## 04 - 会员 & 设备

| 编号 | 缩写 | 名称 | 说明 | 负责人 |
|---|---|---|---|---|
| gp005_ma-web | ma-web | 会员服务 | 会员信息存储/查询/校验，储值账户开立、状态变更与查询 | 沈纲领 |

## 05 - 渠道

| 编号 | 缩写 | 名称 | 说明 | 负责人 |
|---|---|---|---|---|
| gp002_cmf | cmf | 资金渠道管理 Channel Management Foundation | 统一支付接口与资金渠道管理、路由、补单（fund-in / fund-out） | 王迁 |
| gp002_cmf-task | cmf-task | CMF Task | 与渠道订单相关的定时任务 | - |
| gp039_fcw | fcw | 资金渠道回调站点 / Fund Channel Web book | 接收银行/第三方渠道支付结果通知的统一回调系统 | 王迁 |
| gp221_qpay-cko | - | fund-in 渠道适配 | fund-in channel adaptor 之一 | - |
| gp062_h2h | - | fund-out 渠道适配 | fund-out channel adaptor 之一 | - |
| gp016_outman | outman | 外部验证渠道服务 | - | 王迁 |
| gp070_csimple | csimple | 简单渠道 | 对接简单非内部服务（如 totok） | 喻赛 |

## 06 - 清结算

| 缩写 | 名称 | 说明 | 负责人 |
|---|---|---|---|
| counter | 资金管理平台 | 清算操作平台：账务、资金对账、补单、出款、账户科目/会员查询管理 | 王迁 |
| - | 资金渠道管理 & 渠道对账 | - | 王迁 |
| - | 会计系统 | 提供科目、会计相关支持，操作界面落地在 counter | 周聪 |

## 07 - 业务工具

| 编号 | 缩写 | 名称 | 说明 | 负责人 |
|---|---|---|---|---|
| gp003_pbs | pbs | 算费系统 | 计算每笔交易手续费；支持固定费用/费率、阶梯、累计阶梯等收费模式 | 陆亚东 |
| - | pbs-bos | 算费支撑系统 | - | 黄美美 |
| - | mns | 短信发送系统

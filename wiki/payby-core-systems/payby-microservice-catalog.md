---
title: PayBy 全量微服务清单
domain: payby-core-systems
kind: wiki_page
slug: payby-microservice-catalog
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PCW/124555769
tags: []
---

# PayBy 全量微服务清单

本页汇总 PayBy 全部微服务，包括 OPS 团队当前维护的活跃服务清单，以及历史归档的 Deprecated 全量清单（按业务归类）。收单交易相关服务详见 [[acquire-services-catalog]]。

## 活跃服务（Managed by OPS team）

### 网关与接入
- **gp024_cgs** — Client Gateway Service：为 SDK client 或 H5 暴露 HTTP API，按配置路由到各业务服务；包含签名校验、加解密转换、限流等。

### 钱包与社交支付应用
- **gp032_personal** — 提供 top-up、withdrawal 等各类钱包服务。
- **gp053_transfer** — 提供 wallet transfer、split bill、red packet 等转账类业务能力。

### 充值与提现
- **gp011_deposit** — 提供面向 wallet、vis、kiosk 的基础 deposit(top-up) API，同时承担 top-up 业务服务。
- **gp012_fundout** — 提供面向 wallet 与 merchant 的基础 fundout API，同时承担 withdraw 业务服务。

### 交易与收银台
- **gp123_tradeii** — 为需要 trade 与 payment 的业务服务提供基础 trade API；支持需要/不需要 checkout 的支付场景。
- **gp193_cashierii** — 提供面向 app、paypage、pos 的 checkout 相关 API；含风险识别、商户鉴权与支付流程。
- **gp007_cashdesk-api** — 旧版收银台服务，多数功能已被 cashierii 替代；不含 cashier withdraw 流程。

### 风控
- **gp079_grc-component-connect-provider** — 为支付与非支付场景提供风控服务。

### 支付中台
- **gp014_pfs-payment** — 与 payment 协同，为支付接入提供更具体的 API。
- **gp006_payment** — 提供支付流程控制与清结算规则配置。
- **gp004_dpm-accounting** — 提供记账能力：科目与账户管理、复式记账、缓冲入账。

### 资金渠道
- **gp002_cmf** — Channel Management Foundation：管理 fund-in / fund-out 资金渠道。
- **gp002_cmf-task** — CMF 配套定时任务，处理渠道订单相关调度。
- **gp039_fcw** — 资金渠道 web book 服务，接收资金渠道方支付结果回调。
- **gp221_qpay-cko** — fund-in 渠道适配器之一。
- **gp062_h2h** — fund-out 渠道适配器之一。

## Deprecated 全量历史清单

> 以下列表已不再更新，仅作历史归档参考。按归类列出系统编号、缩写、中文名称、英文全名与系统说明。

### 01-网关
- **gp013_pns** — pns / 商户通知服务 / Partner Notify Service：商户通知服务。
- **sgs** — 服务端网关 / Server Gateway：接收商户后台服务器请求。
- **cgs** — 客户端网关 / Client Gateway：接收用户浏览器和手机应用请求。

### 02-应用
- **gp076_market-order** — market-order / 公共事业缴费-订单系统。
- **gp075_market-goods** — market-goods / 公共事业缴费-商品系统。
- **gp074_life-center** — life-center / 公共事业缴费-前置 / Life Center。
- **gp098_green-points** — green-points / 积分应用：各大承运商积分对接平台，积分发行销毁入口。
- **acquire service** — 收单服务 / Acquire Service。
- **gp032_personal** — personal / 个人应用 / Personal。
- **gp027_paycode-pcm** — pcm / 付款码应用 / PayCode Manager：付款码管理，含密钥上传、刷新、查询。
- **gp035_socialpay** — socialpay / 社交支付应用 / Social Pay（开发中）：红包、AA 收款等，调用 transfer 完成业务逻辑。
- **gp053_transfer** — transfer / 转账服务（开发中）：转账、结算、退款等核心能力，调用 trade 完成交易。
- **gp007_cashdesk-api** — cashdesk-api / 收银台。

### 03-支付中台
- **gp010_trade** — trade / 交易服务。
- **gp011_deposit** — deposit / 存款服务。
- **gp012_fundout** — fundout / 出款服务。
- **gp014_pfs-payment** — pfs-payment / 支付前置-支付服务：定义可扩展业务支付 API，存储支付基础信息，对业务支付订单做校验与增强，持久化业务订单领域，并基于订阅发送统一支付结果消息。
- **gp014_pfs-basis** — pfs-basis / 支付前置-对外基础服务。
- **gp014_pfs-manager** — pfs-manager / 支付前置-后台管理服务。
- **gp006_payment** — payment / 支付引擎：依据支付服务定义、参与方清结算协议等，控制支付指令处理流程；对成功指令做债权债务清分与最终资金划拨。
- **gp004_dpm-accounting** — dpm-accounting / 储值-记账：账户信息存储与交易明细记录；借贷分离账户体系；三种基于账户属性的入账规则；配套入账与账户查询管理接口。
- **gp004_dpm-task** — dpm-task / 储值-批量任务：处理缓冲入账等批量任务。
- **gp004_dpm-manager** — dpm-manager / 储值-管理接口：开户、查询等账户管理服务。

### 04-会员&设备
- **gp005_ma-web** — ma-web / 会员服务：会员信息存储/查询/验证，及储值账户开立、状态变更与查询。

### 05-渠道
- **gp002_cmf** — cmf / 资金渠道管理：统一支付接口、资金渠道统一管理与路由，及补单功能。
- **gp016_outman** — outman / 外部验证渠道服务。
- **fcw** — 资金渠道回调站点：银行或第三方渠道支付结果统一回调系统。
- **gp070_csimple** — csimple / 简单渠道：对接非内部的简单服务（如 totok）。

### 06-清结算
- **counter** — 资金管理平台：清算人员操作平台，处理账务、资金对账、补单、出款、账户科目会员查询管理。
- **资金渠道管理 & 渠道对账**。
- **会计系统**：科目与会计相关支持，实操界面可落地于 counter。

### 07-业务工具
- **pbs-bos** — 算费支撑系统。
- **mns** — 短信发送系统：邮件、手机短信、微博通知，支持定时与 freemarker 模板；提供 RestAPI 与 Java 客户端 jar。
- **mns-mq-listener** — mns 的 MQ 监听器。
- **mns-scheduler-web** — mns 定时任务。
- **mns-admin** — 短信发送管理系统。
- **gp003_pbs** — pbs / 算费系统：按商户合同收费模式（固定费用/费率、阶梯、累计阶梯）与算费请求订单金额，计算指定付费方手续费。

---
title: PayBy 服务分类地图
domain: payby-core-systems
kind: wiki_page
slug: payby-service-category-map
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:2bc88b9d-fdd4-46f9-a4aa-7ef0774c7418
tags: []
---

# PayBy 服务分类地图

按十大类组织 PayBy 内部系统的导航视图，便于按职责定位服务。完整服务清单见 [[payby-microservice-catalog]]，当前活跃子集见 [[payby-active-microservices]]。

## 01 - 网关
- `gp013_pns` pns 商户通知服务（Partner Notify Service）
- `sgs` 服务端网关（Server Gateway）：接收商户后台服务器请求
- `cgs` 客户端网关（Client Gateway）：接收用户浏览器和手机应用请求；含签名验证、加解密转换、限流等

## 02 - 应用
- `gp076_market-order` market-order 公共事业缴费 - 订单系统
- `gp075_market-goods` market-goods 公共事业缴费 - 商品系统
- `gp074_life-center` life-center 公共事业缴费 - 前置（Life Center）
- `gp098_green-points` green-points 积分应用：承运商积分对接、积分发行/销毁入口
- `acquire service` 收单服务
- `gp032_personal` personal 个人应用：钱包充值、提现等
- `gp027_paycode-pcm` pcm 付款码应用：付款码上传密钥、刷新、查询等管理
- `gp035_socialpay` socialpay 社交支付应用：红包、AA 收款，调用 transfer
- `gp053_transfer` transfer 转账服务：转账、结算、退款；钱包转账、拆单、红包
- `gp007_cashdesk-api` 收银台（旧版，多数功能已被 cashierii 替代，不含 cashier withdraw 流程）

## 03 - 支付中台
- `gp010_trade` / `gp123_tradeii` trade / tradeii 交易服务：基础 trade API，支持需/不需 checkout 的支付场景
- `gp011_deposit` deposit 存款/充值服务：wallet、vis、kiosk 通用 top-up
- `gp012_fundout` fundout 出款/提现服务：wallet 与 merchant 通用 withdraw
- `gp193_cashierii` cashierii 收银台：app/paypage/pos checkout，含风险识别、商户鉴权、支付流程
- `gp014_pfs-payment` pfs-payment 支付前置 - 支付服务：可扩展业务支付 API，业务校验/增强、持久化订单、统一支付结果消息
- `gp014_pfs-basis` pfs-basis 支付前置 - 对外基础服务
- `gp014_pfs-manager` pfs-manager 支付前置 - 后台管理服务
- `gp006_payment` payment 支付引擎：控制支付指令处理流程、清分与资金划拨；清结算规则配置
- `gp004_dpm-accounting` dpm-accounting 储值 - 记账：账户信息、借贷分离账户、双分录、缓冲入账
- `gp004_dpm-task` dpm-task 储值 - 批量任务：缓冲入账等批处理
- `gp004_dpm-manager` dpm-manager 储值 - 管理接口：开户、查询等账户管理

## 04 - 会员 & 设备
- `gp005_ma-web` ma-web 会员服务：会员信息存储/查询/验证、储值账户开立与状态变更

## 05 - 渠道
- `gp002_cmf` cmf 资金渠道管理：统一支付接口、渠道路由、补单
- `gp002_cmf-task` cmf-task：渠道订单相关定时任务
- `gp016_outman` outman 外部验证渠道服务
- `gp039_fcw` fcw 资金渠道回调站点：统一接收银行/第三方支付结果通知
- `gp070_csimple` csimple 简单渠道：对接 totok 等非内部简单服务
- `gp221_qpay-cko` 资金 fund-in 渠道适配器
- `gp062_h2h` 资金 fund-out 渠道适配器

## 06 - 清结算
- `counter` 资金管理平台：清算操作，账务/对账/补单/出款/账户科目/会员查询管理
- 资金渠道管理 & 渠道对账
- 会计系统：科目与会计支持（操作界面可落地于 counter）

## 07 - 业务工具
- `pbs-bos` 算费支撑系统
- `mns` 短信发送系统：邮件/短信/微博通知，定时发送，freemarker 模板，REST API + Java 客户端 jar
- `mns-mq-listener` 短信发送 MQ 监听器
- `mns-scheduler-web` 短信发送定时任务
- `mns-admin` 短信发送管理
- `gp003_pbs` pbs 算费系统：固定费用|费率、阶梯费用|费率、累计阶梯，按合同与付费方计费
- `gp017_nffs` nffs 新流量系统
- `gp042_pcs` pcs 付款码生成工具
- `gp034_authpay` authpay 收银台鉴权
- `gp008_acs` acs 商户协议配置服务
- `gp009_voucher` voucher 凭证服务
- `gp056_csc` csc 运营对账系统：跨服务业务数据完整性/正确性核对报警
- `query` 统一查询服务
- `gp040_pts` pts 个人 token 服务：跨系统 token，主要用于登录
- 付款码服务

## 08 - 风控
- `gp079_grc-component-connect-provider` 风控组件接入：支付与非支付风控
- `gp015_limit` limit 限额限次
- 风控系统

## 11 - 内部运营平台
- `gp023_basis` basis 基础管理后台：业务运营为主，含少量开发操作（如 CSA 对账）
- `gp091_cms` cms 一期后端
- `gp094_basis-cms` basis-cms cms 前端：内容管理
- `gp126_cmsii` cmsii cms 二期：内容管理、白名单、布局等

## 99 - 中间件
- `gp001_ues` ues-ws 统一加密：关键数据加密为可见 Ticket，业务可基于 Ticket（可携带 MASK 数据）操作而不触碰原始数据
- `ues-console` 统一加密控制台
- `dubbo-admin` 管理控制台
- `elasticjob-console` 统一调度
- `ufs` 统一文件

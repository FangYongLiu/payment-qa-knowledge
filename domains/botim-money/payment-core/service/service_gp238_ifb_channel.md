---
id: svc_ifb_channel
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp238
name: ifb-channel
dev_owner: Yadong.Lu
aliases: [gp238_ifb-channel]
related_services: []
related_tables: []
---

# ifb-channel

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp238` · domain=`payment-core`。

## 作用
**IFB 汇款渠道**接入服务(gp238,UAT 近7d ~35 万条)。对接 IFB 渠道做汇款出款/查询/余额,属**汇款(remittance)渠道**而非即时支付。

## 系统中的位置
- 功能层:渠道接入(Remittance Channel)
- 业务域:`payment-core`(渠道接入;业务归属 remittance)

## 关联关系
实测 mClass:`DefaultRemChannelFacadeImpl`(汇款渠道门面)、`RemittanceClient`(调汇款核心)、`SingleDetailQueryRequester`/`QueryBalanceRequester`(明细/余额查询)、`DefaultChannelCallbackFacadeImpl`(渠道回调)。服务于跨境汇款渠道链路(remittance 域)。

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp238` · domain=`payment-core`。

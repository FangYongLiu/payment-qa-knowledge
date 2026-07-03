---
id: svc_adtaxi
object_type: Service
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp125
name: adtaxi
dev_owner: Sijia.Zhang
aliases: [gp125_adtaxi]
related_services: []
related_tables: []
---

# adtaxi

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp125` · domain=`online-business`。

## 作用
**出租车 ITC 码扫码支付**服务(gp125)。UAT 实测为收单域**流量最大**的应用(近7d ~1640 万条日志)。以**订单状态机 + 定时推进 job + 收单事件监听**驱动出租车支付订单生命周期。

## 系统中的位置
- 功能层:收单业务线(出租车 / ITC 扫码支付)
- 业务域:`online-business`
- 驱动方式:事件(MQ)+ 定时 job,非同步 RPC(本窗口无 `*ClientImpl`)。

## 关联关系
**事件驱动**:`AcquireEventListener` 监听 [[svc_acquireii]] 的收单事件(支付结果)→ 推进本地出租车订单;MQ 消费异常走 `RejectAndDontRequeueRecoverer`(拒绝且不重入队)。无同步 RPC 下游(本窗口)。

## 关键方法 / 入口(UAT 实测 mClass)
- `AdTaxiOrderPaidAutoAdvanceJob` —— 已支付订单自动推进。
- `AdTaxiOrderAutoAdvanceJob` —— 订单状态机定时推进。
- `AcquireEventListener` —— 监听收单支付事件。
- `RejectAndDontRequeueRecoverer` —— MQ 消费失败恢复策略。

## 测试要点 / 排障 / 常见问题
- **订单状态机推进**:验证 AutoAdvanceJob 按预期把订单从待支付→已支付→完成推进;job 幂等与重复执行。
- **事件消费**:收单支付事件到达后订单是否正确推进;MQ 消费失败是否走 `RejectAndDontRequeue`(不无限重试)。
- 落库 `adtaxi` 库(见下「涉及的表」)订单状态一致性。

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp125` · domain=`online-business`。

## 涉及的表(DB)
本服务读写 `adtaxi` 库(9 张,见 `online-business/table/adtaxi/`)。主要表:[[tbl_adtaxi_t_adtaxi_order]]。

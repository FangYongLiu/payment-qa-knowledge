---
id: svc_device
object_type: Service
domain: offline-business
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp054
name: device
dev_owner: Shuo.Wang
aliases: [gp054_device]
related_services: [svc_ppcenter, svc_merchant]
related_tables: []
---

# device

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp054` · domain=`offline-business`。

## 作用
设备 / 产品中心接入（调 ppcenter/merchant/store）

## 系统中的位置
- 功能层:营销 / 产品 / 报价 (Marketing / Product / Quote)
- 业务域:`offline-business`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_ppcenter]] ppcenter（产品中心） · 361089 次 · high
- [[svc_merchant]] merchant（商户主数据 / 商户管理） · 9066 次 · high

**被调用(上游)—— 这些服务调用本服务:**
acquireii

## 涉及的 API / 数据库表
**读写的表:** [[tbl_device_apply_order]] 设备申请订单表、[[tbl_device_db]] 设备库(device)核心表

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[flow_device_activation]](流程:设备激活端到端流程(Smart POS))
- [[scn_pos_transaction_db_check]](场景:POS刷卡交易落库检查)

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp054` · domain=`offline-business`。

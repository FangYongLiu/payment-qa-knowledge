---
id: svc_life_center
object_type: Service
domain: payment-tools
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp074
name: life-center
dev_owner: Guoyou.Ma
aliases: [gp074_life-center]
related_services: []
related_tables: []
---

# life-center

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp074` · domain=`payment-tools`。

## 作用
(本窗口未观测到该服务的运行时活动,作用待业务补充。)

## 系统中的位置
- 业务域:`payment-tools`

## 关联关系
(本窗口未观测到与其它服务的调用关系)

## 参与的业务场景(cgs 回归)
- §10. 红包 / 社交支付、生活缴费、VAM（toC：`test_red_pkg` / `test_friend_transfer` / `test_vam` / 充值）

## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 相关流程 / 场景 / 排障(反向)
本服务涉及的流程/场景/排障(由对方 `related_services` 指向,反向汇总):
- [[flow_life_center_mobile_topup]](流程:Life Center 话费充值端到端流程(SGS))
- [[flow_remittance_life_center_sgs_query]](流程:Life-Center SGS 预付国际商品 / 后付费账单查询调用链)
- [[scn_life_center_mobile_topup]](场景:Mobile Top-up 话费充值(SGS))

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp074` · domain=`payment-tools`。

---
id: svc_tts
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp311
name: tts
dev_owner: Qian.Wang
aliases: [gp311_tts]
related_services: []
related_tables: []
---

# tts

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp311` · domain=`payment-core`。

## 作用
(本窗口未观测到该服务的运行时活动,作用待业务补充。)

## 系统中的位置
- 业务域:`payment-core`

## 关联关系
(本窗口未观测到与其它服务的调用关系)

## 涉及的 API / 数据库表
- **暴露 API**(Dubbo,来源 `tts-dubbo-api` 文档):**分期(Installment)**——`InstallmentFacade`(`queryPlanList` 按卡+金额查可用分期方案 / `confirmInstallment` 确认分期(授权码+支付)/ `cancelInstallment` / `refundInstallment` / `queryInstallmentOrder`)。
- **读写的表**:分期订单/方案(具体对象待补)。

## 关键方法 / 入口
- 待补(本窗口未单独抽取 Dubbo/RPC 方法级)。

## 测试要点 / 排障 / 常见问题
- 待补(QA 视角:怎么测、已知坑、典型故障与定位)。

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp311` · domain=`payment-core`。

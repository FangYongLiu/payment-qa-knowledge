---
id: svc_ues_ws
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp001
name: ues-ws
dev_owner: Yongxing.Cao
aliases: [gp001_ues-ws]
related_services: []
related_tables: []
---

# ues-ws

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp001` · domain=`payment-core`。

## 作用
用户事件 / 数据服务（saveDataByParam）—— 被收银 / 渠道 / 通知调用

## 系统中的位置
- 功能层:通知 / 消息 (Notification)
- 业务域:`payment-core`

## 关联关系

**被调用(上游)—— 这些服务调用本服务:**
wechat-channel, merchant-frontend, mns-main, escrow, acquireii, cashdesk-api

## 关键方法 / 入口
**UAT Kibana 7d INFO 观测的主要业务类**(app_id=`ues-ws`,=实际在跑的业务操作 / 入口):
- `NettyServerHandler`×14,327 — Netty 长连接服务
- `UpdateCertificationRoutine`×4,033 — 证书更新
- (类名为 Dubbo/RPC 处理器/门面;次数为 7d 调用量级,反映主链路。)
## 涉及的 API / 数据库表
- **暴露/相关 API**:待补
- **读写的表**:待补

## 测试要点 / 排障 / 常见问题

**UAT Kibana 7d 错误观测**(自动回归 + UAT 流量,app_id=`ues-ws`):
- ERROR 0(7d 无)
- WARN 3 次(均为基础设施噪声)
- ⚠️ 频次可能含 UAT 测试数据噪声,**真坑 vs 噪声需人工确认**;高频项见域级排障对象。
- 更多 QA 校验点(怎么测 / 已知坑 / 典型故障定位)待补。
## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp001` · domain=`payment-core`。

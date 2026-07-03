---
id: svc_npss_gateway
object_type: Service
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-23'
source_type: app_inventory
source_ref: SYSTEM_APP_INVENTORY.md
tags: []
app_group: gp210
name: npss-gateway
dev_owner: Qian.Wang
aliases: [gp210_npss-gateway]
related_services: [svc_npss]
related_tables: []
---

# npss-gateway

> 来源:UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp210` · domain=`payment-core`。

## 作用
NPSS（即时支付系统）报文网关

## 系统中的位置
- 功能层:接入网关 / 前端 BFF (Gateway / Frontend)
- 业务域:`payment-core`

## 关联关系
**调用(下游)—— 本服务依赖:**
- [[svc_npss]] npss（即时支付 / 账单） · 17610 次 · high

**被调用(上游)—— 这些服务调用本服务:**
npss, qpay-npss

## 参与的业务场景(cgs 回归)
- §8. 账单 / 即时支付（`test_ppcTransaction`，NPSS）

## 涉及的 API / 数据库表
- **暴露/相关 API**:NPSS 报文收发网关;`NpssClientImpl`(调 [[svc_npss]])、`MqClientImpl`/`MqFacadeImpl`(MQ 收发)、`OidcController`/`OidcServiceImpl`(OIDC 认证)、`OverlayBackEndController`。
- **读写的表**:报文 / 会话(具体对象待补)。

## 关键方法 / 入口(UAT 实测 mClass)
- `NpssClientImpl` —— 与 [[svc_npss]] 核心交互。
- `MqClientImpl` / `MqFacadeImpl` —— NPSS 报文经 MQ 收发。
- `OidcController` / `OidcServiceImpl` —— OIDC 认证(NPSS 网络接入鉴权)。
- `OverlayBackEndController` —— Overlay 后端接口。

## 测试要点 / 排障 / 常见问题(UAT 实测)
- **报文网关职责**:NPSS 对外报文的收发 + OIDC 认证入口;业务在 [[svc_npss]]。
- **怎么测/定位**:即时支付报文异常先分清"卡在网关(OIDC 认证/MQ 收发)"还是"到了 npss 核心";OIDC 鉴权失败即报文被拦。

## 来源与置信
- UAT Kibana trace, last 120d 宽窗口采样(2026-06-24) + 作用说明。候选待人审。app_group=`gp210` · domain=`payment-core`。

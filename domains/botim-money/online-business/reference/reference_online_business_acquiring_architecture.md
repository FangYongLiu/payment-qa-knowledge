---
id: reference_online_business_acquiring_architecture
object_type: Reference
name: 线上收单架构分层总览 (Online Acquiring Architecture)
aliases: [收单架构, acquiring architecture, online-business 分层]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: manual
source_ref: online-business 架构梳理
tags: [online-business, 收单, 架构, gateway, facade, acquire]
related_services: [svc_sgs, svc_customer_frontend, svc_merchant_console_frontend, svc_acquireii, svc_acquire2_query, svc_statementii, svc_merchant_settlement]
---

# 线上收单架构分层总览 (Online Acquiring Architecture)

线上收单(online-business)链路的分层视图。这是一条**跨团队域**的调用链:入口与收单核心归 online-business,商户主数据归 [[domain_merchant_management]],通知等共享能力归 [[domain_infrastructure]]。本页按架构层汇总各服务并跨域链接;各服务的权属仍以其所在域为准。

## 分层

### 网关层 (Gateway)
- [[svc_sgs]](gp028)server-gateway-service —— 服务端网关:签名验证、权限控制、限流。ToB 收单入口(ToC 走 payment-core 的 cgs)。**@online-business**

### Facade 层
- [[svc_merchant_frontend]](gp071)线上收单 Facade —— 线上交易处理、请求路由、参数校验。**@merchant-management**
- [[svc_customer_frontend]](gp064)客户 Facade —— APP 交易聚合、参数校验、请求路由。**@online-business**
- [[svc_merchant_console_frontend]](gp045)商户控台前端。**@online-business**

### 核心业务层 (Core Business)
- [[svc_acquireii]](gp069)收单核心服务 2.0 —— 订单状态管理、业务流程控制、交易数据传输。**@online-business**
- [[svc_acquire2_query]](gp275)收单查询服务。**@online-business**

### 商户服务层 (Merchant)
- [[svc_merchant]](gp044)商户核心服务 (Merchant Core)。**@merchant-management**
- [[svc_basis_merchant]](gp161)业务运营后台管理。**@merchant-management**
- [[svc_contract]](gp107)商户合同。**@merchant-management**
- [[svc_pns]](gp013)商户通知服务 (Partner Notify Service)。**@infrastructure**

### 财务 / 结算层 (Finance / Settlement)
- [[svc_statementii]](gp134)对账服务 —— 生成对账文件、结算文件、交易对账。**@online-business**
- [[svc_merchant_settlement]](gp288)结算服务 —— MPGS 商户直连、独立结算流程、资金清算。**@online-business**

## 调用链(高层)
```
商户 / APP
   │  ToB 收单请求
   ▼
[Gateway] svc_sgs —— 验签 / 鉴权 / 限流
   │
   ▼
[Facade] merchant-frontend / customer-frontend / merchant-console-frontend —— 路由 / 参数校验 / 聚合
   │
   ▼
[Core] svc_acquireii —— 收单订单状态机与流程控制(查询走 acquire2-query)
   │        ├─ 商户主数据校验 → [Merchant] svc_merchant / svc_basis_merchant / svc_contract
   │        └─ 结果通知 → svc_pns
   ▼
[Settlement] svc_statementii(对账)/ svc_merchant_settlement(结算 / MPGS 直连)
```

## 说明
- **跨域**:商户核心 / 运营后台 / 合同属 [[domain_merchant_management]](Chahid 团队);通知服务 pns 属 [[domain_infrastructure]]。本页仅做架构汇总,不改变其归域。
- 收单库表见 `online-business/table/acquireii/`(acquire-service 2.0 数据);对账 / 结算见 `statementii` 相关表。
- 端到端交易时序(含 DB 校验点)见本域 `flow/` 与 `scenario/`。

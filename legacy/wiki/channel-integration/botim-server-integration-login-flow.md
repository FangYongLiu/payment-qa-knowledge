---
title: Botim服务端集成-登录流程
domain: channel-integration
kind: wiki_page
slug: botim-server-integration-login-flow
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:80e249f0-da50-4572-b397-a7d1c4b13711
tags: []
---

# Botim服务端集成-登录流程

本页描述 Botim App 登录并联动 PayBy 登录的端到端时序：先在 Botim 自有服务完成认证，再经 sgs 网关进入 personal 服务，由其编排设备落库、静默登录与风控咨询，最终将 accessToken 返回客户端。

## 参与方

- app use（终端用户）
- botim app（客户端）
- botim server（Botim 服务端）
- sgs（PayBy 网关）
- personal（个人服务，登录编排）
- pts（设备服务）
- member（会员服务）
- cps（风控服务）

## 主流程时序

1. `login`：app use → botim app
2. `botim login`：botim app → botim server
   - `verified`：botim server 自校验
3. `payby login`：botim app → botim server
4. `/personal/v3/auth/login`：botim server → sgs
5. `with device info`：sgs → personal（携带设备信息）

## personal 内部编排（1.2.1.1.x）

personal 在收到登录请求后，依次执行：

1. `checkAvailable`：personal 自检可用性
2. `IDefaultDeviceFacade#save`：personal → pts，保存设备
3. `AccessTokenFacade#silentLogin`：personal → member，静默登录
4. `ConsultRiskServiceStub#consultRiskManager`：personal → cps，风控咨询
5. `accessToken`：personal → sgs（返回）

## 返回链路

- sgs → botim server（返回登录结果）
- botim server → botim app（返回 accessToken 等）

## 关键说明

- Botim 侧认证（`botim login` / `verified`）与 PayBy 侧登录（`payby login`）是两段独立但顺序衔接的流程。
- PayBy 登录入口固定为网关路径 `/personal/v3/auth/login`，由 sgs 透传至 personal。
- personal 是登录编排中枢，分别协同 pts（设备）、member（令牌）、cps（风控）三方完成。

---
title: 收单交易相关应用服务清单
domain: acquire-transaction
kind: wiki_page
slug: acquire-services-catalog
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:a8df82dd-8926-4122-b8c0-981d2facbbf8
tags: []
---

# 收单交易相关应用服务清单

本页汇总收单链路涉及的微服务应用、用途说明与负责人，便于在排查交易、对接联调时快速定位。完整业务背景见 [[acquire-transaction-overview]]。

## 应用清单

| Application | Description | Owner |
|---|---|---|
| gp028_sgs | 服务端网关 / Server gateway service | 喻赛 |
| gp071_merchant-frontend | 商户服务-sgs前置 | 王斌 |
| gp069_acquireii | 商户收单服务 | 王斌 |
| gp193_cashierii | 收银台v2 | 刘智斌 |
| gp007_cashdesk-api | 收银台api / Cashdesk service | 刘智斌 |
| gp123_tradeii | 交易服务 / Trade service | 唐宇 |
| gp079_grc | 核身查询 | 李德文 |
| gp034_authpay | 支付鉴权 / Payment authentication | 刘智斌 |
| gp003_pbs | 算费服务 | 黄美美 |
| gp044_merchant | 商户服务 | 黄林伟 |
| gp005_member | 会员服务 / Member service | 陆亚东 |
| gp083_merchant-fundout | 商户出款应用 | 王斌 |
| gp004_dpm | 储值记账 | 周聪 |
| gp209_aml | 风控 | 李德文 |
| gp014_pfs-payment | 支付前置 / Payment front service | 李德文 |
| gp006_payment | 支付引擎 / Payment engine service | 李德文 |
| gp002_cmf | 资金渠道管理 | 张鹤飞 / 马国友 |
| gp124_router | 渠道路由 | 马国友 |
| gp267_qpay-mpgs | MPGS渠道 | 马国友 |
| gp039_fcw | 机构通知回调 | 马国友 |
| gp043_reconciliation | 清算 | 夏一冰 |
| gp031_counter | 清算管理后台 | 夏一冰 |

## 按链路环节归类

- **接入层**：`gp028_sgs`、`gp071_merchant-frontend`
- **收单与交易**：`gp069_acquireii`、`gp123_tradeii`
- **收银台与鉴权**：`gp193_cashierii`、`gp007_cashdesk-api`、`gp034_authpay`
- **风控与核身**：`gp079_grc`、`gp209_aml`
- **商户与会员**：`gp044_merchant`、`gp005_member`、`gp083_merchant-fundout`
- **计费与记账**：`gp003_pbs`、`gp004_dpm`
- **支付引擎与渠道**：`gp014_pfs-payment`、`gp006_payment`、`gp002_cmf`、`gp124_router`、`gp267_qpay-mpgs`、`gp039_fcw`
- **清算**：`gp043_reconciliation`、`gp031_counter`

## 系统组件总览

下表从更宏观的系统视角梳理收单及相关周边的组件分组，便于了解上下游接入关系。组件类型分为：合作方组件、jar 组件、静态资源、内部应用。

### 组件分组

- **商户 (Merchant)**：商户管理员、pos机、小白盒
- **静态资源 (Static resources)**：hive-merchant、hive-m-topay
- **网关 (Gateway)**：pos-gateway、xbh-gateway、cgs、sgs
- **SDK 平台 (SDK platform)**：app-sdk（jar 组件）、平台服务端
- **收单 (Acquiring)**：software-management、merchant-console-frontend、device、acquire-service、merchant
- **个人 (Personal)**：pcm、socialpay、personal、transfer
- **公共 (Public/Common)**：pts

### 主要依赖关系

- 商户管理员 → `hive-merchant`（静态资源）
- 商户管理员 → `merchant-console-frontend`
- pos机 → `pos-gateway`
- 小白盒 → `xbh-gateway`
- app-sdk → `cgs`；app-sdk → `hive-m-topay`
- 平台服务端 → `sgs`
- `pos-gateway` → `acquire-service`
- `xbh-gateway` → `acquire-service`；`xbh-gateway` → `device`

> 说明：上述系统组件视图与「应用清单」中的 gp 应用为不同维度的命名。其中网关侧的 `sgs` 对应 `gp028_sgs`，收单侧的 `acquire-service`、`merchant`、`merchant-console-frontend` 与 `gp069_acquireii`、`gp044_merchant`、`gp071_merchant-frontend` 在职责上对应。

## 相关参考

- 接入侧场景标识见 [[acquire-pay-scene-code]]
- 渠道侧标识见 [[acquire-pay-channel-no]]
- 各应用对应的库表查询见 [[acquire-database-guide]]

---
id: tbl_cashdesk_t_filter_node
object_type: Table
domain: channel-integration
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki
source_ref: confluence:AQ/2228977707
tags:
- payment-auth
- preferSign
- config
subdomain: cashdesk
module: payment-auth
sensitivity: normal
name: 支付鉴权配置表 t_filter_node
aliases:
- t_filter_node
related_services: []
related_tables: []
related_scenarios:
- scn_cko_subscription_test_cards
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
支付鉴权配置表，位于 `cashdesk` 库。用于存放 authpay 支付鉴权规则及 `preferSign` 配置，决定 CKO 订阅支付路由时是否优先签约。配置由专属人员根据实际投产情况统一维护，测试环境与生产保持一致，测试人员不可随意更改。

## 关键列
- `unit_id`：区分支付绑卡场景
  - `unit_id=13`：已绑卡（card_pay）
  - `unit_id=4`：新绑卡（quick_pay）
- `preferSign`（鉴权返回字段，取值）：
  - `Y` — 优先签约 / 订阅
  - `N` — 明确配置为不优先签约
  - `Null` — 未命中 / 未配置该字段，按不签约处理

## 主键/索引
原文未提供。

## 校验点(QA 关注)
- 商户 `200000036054` 一般已满足收单要求；如鉴权不满足，需联系配置负责人协助调整，**禁止测试人员自行修改**。
- 鉴权按商户组、产品码、支付场景、入口、版本号匹配，命中后返回 `preferSign`，并区分 `card_pay`（已绑卡 unit_id=13）/ `quick_pay`（新绑卡 unit_id=4）。
- `paychannel` 维度：`15` 本地卡 / AE，`30` 外卡。
- 配置结果会被缓存于 `paymentMethod`（`/cashdesk/unityInitPayPage` 调用 authpay 后），后续 `confirmPayInfo`、`verify` 阶段以此判定 `preferSign` 与 `frictionless` 传参。
- 全局配置 `alwaysPreferSign=true` 且借记卡时，将忽略本表 `preferSign` 结果，强制 `preferSign=Y`（老收银台 `cashdesk-api.yml`，新收银台 `gp193_cashierii.yml`）。
- 测试时需关注：鉴权命中规则与 `preferSign` 取值是否与预期一致，否则路由结果（CKO101/102/111）会偏离预期。

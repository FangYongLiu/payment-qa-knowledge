---
id: tbl_cashdesk_t_filter_node
object_type: Table
name: 支付鉴权配置表 (cashdesk.t_filter_node)
aliases: [t_filter_node]
domain: payment-tool
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/2228977707
tags: [cko, payment-auth, preferSign, config]
related_services: [svc_qpay_cko]
related_scenarios: [scn_cko_subscription_payment]
---

# 支付鉴权配置表 (cashdesk.t_filter_node)

## 用途
支付鉴权配置表，位于 `cashdesk` 库。用于存放 authpay 支付鉴权规则及 `preferSign` 配置，决定 CKO 订阅支付路由时是否优先签约。配置由专属人员根据实际投产情况统一维护，测试环境与生产保持一致，**测试人员不可随意更改**。

## 关联关系
- **所属服务**:[[svc_qpay_cko]](= frontmatter `related_services`)
- **谁读写它**:收银台 cashdesk / cashierii 在 `unityInitPayPage` / `confirmPayInfo` / `verify` 阶段读取(待补:收银台服务对象尚未建,见正文)。
- **哪些场景校验它**:[[scn_cko_subscription_payment]](= `related_scenarios`)。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `unit_id` | - | 区分支付绑卡场景:`13`=已绑卡(card_pay),`4`=新绑卡(quick_pay) |
| `preferSign` | - | 鉴权返回字段:`Y`优先签约/订阅,`N`明确不优先签约,`Null`未命中按不签约处理 |
| `paychannel` | - | `15`本地卡 / AE,`30`外卡 |

## 主键 / 索引
- 待补:原文未提供。

## 校验点(QA 关注)
- 商户 `200000036054` 一般已满足收单要求;鉴权不满足时联系配置负责人,**禁止测试人员自行修改**。
- 鉴权按商户组、产品码、支付场景、入口、版本号匹配,命中后返回 `preferSign`,并区分 `card_pay`(unit_id=13)/`quick_pay`(unit_id=4)。
- 配置结果缓存于 `paymentMethod`(`/cashdesk/unityInitPayPage` 调 authpay 后),后续 `confirmPayInfo`、`verify` 以此判定 `preferSign` 与 `frictionless` 传参。
- 全局配置 `alwaysPreferSign=true` 且借记卡时,忽略本表 `preferSign`,强制 `preferSign=Y`(老收银台 `cashdesk-api.yml`,新收银台 `gp193_cashierii.yml`)。
- 测试时关注:鉴权命中规则与 `preferSign` 取值是否与预期一致,否则路由结果(CKO101/102/111)会偏离预期。

---
title: 商户收单测试环境与工具
domain: merchant-acquisition-testing
kind: wiki_page
slug: merchant-acquisition-test-environment-and-tools
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:4ef3640b-38b5-4756-81d5-d729c241dc79
tags: []
---

# 商户收单测试环境与工具

本页汇总商户收单测试用到的环境、域名、工具、UAT 测试账号与常用 MID。具体测试方法论见 [[merchant-acquisition-test-methodology-overview]]。

## 环境与域名

| 环境 | 商户后台 | API 域名 | 备注 |
|---|---|---|---|
| SIM | — | 内部使用 | 开发联调环境 |
| UAT | https://uat-web-merchant.test2pay.com/ | https://uat.test2pay.com | 主要测试环境 |
| 生产 | https://b.botim.money/ | https://api.payby.com | 仍是 payby 域名（品牌切换中） |

## 关键工具

| 资源 | 入口 |
|---|---|
| 官方 API 文档 | https://developers.botim.money |
| SGS 接口测试平台 | https://qa.test2pay.com/manualTest/gateway/sgs |
| UAT API Key 配置 | https://uat-web-merchant.test2pay.com/management/api-key |
| SIM 环境 MySQL 链接 | http://gitlab.test2pay.com/dba/passwd/blob/master/mysql.md |
| 常用数据库指南 | 常用数据库指南 |

日志/链路排查可通过 Kibana 按 `traceCode` 全链路检索，`traceCode` 在接口响应 head 中返回；也可登跳板机看应用日志。日志验证细节见 [[merchant-acquisition-e2e-five-stage-verification]]。

## UAT 测试账号

默认 10 个测试用户：

- 手机号：`+971 56 000 0000` ~ `+971 56 000 0009`
- 验证码：`123456`（统一）
- 支付密码：`132580`（统一）

官方测试卡：

| Field | Value |
|---|---|
| Card Number | 5123 4500 0000 0008 |
| Expiry | 05/31 |
| CVV2 | 100 |

更全的测试卡清单（含品牌、地域、DCC、3DS 兜底卡）和触发渠道返回的特殊 expiry，见 [[merchant-acquisition-test-data-conventions]]。

## 测试 MID（部分常用）

| 用途 | UAT MID | 备注 |
|---|---|---|
| 通用 MPGS 商户 | 200000087655 | MPGSID `TEST461000000011` / KEY `P3313662` |
| MPGS 主测商户 | 200000434597 | MPGSID `TEST461000000011` / KEY `P3413282` |
| Device Pay 商户 | 200000434580 / 200000079697 | ApplePay / GooglePay / SamsungPay 测试 |

实际 MID 配置以分配到的具体测试任务和 Confluence 测试账号清单为准。

## 相关

- 调用接口的 curl/Postman 模板：[[merchant-acquisition-curl-postman-skeleton]]
- 域总览：[[domain_merchant_acquisition]]

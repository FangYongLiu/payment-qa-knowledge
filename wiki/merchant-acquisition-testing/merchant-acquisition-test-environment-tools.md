---
title: 商户收单测试环境与工具
domain: merchant-acquisition-testing
kind: wiki_page
slug: merchant-acquisition-test-environment-tools
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2125922317
tags: []
---

# 商户收单测试环境与工具

本页汇总商户收单测试所需的环境域名、平台工具、UAT 测试账号与常用 MID，是开始测试前的环境准备清单。完整测试方法论见 [[merchant-acquisition-test-methodology-overview]]。

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

更多卡号清单（按品牌/地区/DCC 分类）以及触发渠道返回的特殊 expiry 见 [[merchant-acquisition-test-data-preparation]]。

## 测试 MID（部分常用）

| 用途 | UAT MID | 备注 |
|---|---|---|
| 通用 MPGS 商户 | 200000087655 | MPGSID `TEST461000000011` / KEY `P3313662` |
| MPGS 主测商户 | 200000434597 | MPGSID `TEST461000000011` / KEY `P3413282` |
| Device Pay 商户 | 200000434580 / 200000079697 | ApplePay / GooglePay / SamsungPay 测试 |

实际 MID 配置以接到的具体测试任务和 Confluence 测试账号清单为准。

## 配套参考

- 调用骨架（Header / Create Order / Refund / Balance / 对账单下载 curl）：[[merchant-acquisition-curl-postman-templates]]
- 跑通一笔交易后的全链路验证：[[merchant-acquisition-e2e-five-stage-verification]]
- 测试数据命名与金额选择：[[merchant-acquisition-test-data-preparation]]

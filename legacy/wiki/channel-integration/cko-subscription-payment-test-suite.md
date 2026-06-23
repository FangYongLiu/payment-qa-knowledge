---
title: CKO订阅支付测试用例集总览
domain: channel-integration
kind: wiki_page
slug: cko-subscription-payment-test-suite
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_attachment
source_ref: wiki_attachment:af0d55d4-10d6-454b-b0a9-8ff7e104cd04
tags: []
---

# CKO订阅支付测试用例集总览

本页汇总CKO订阅支付测试用例集的整体结构，覆盖新老收银台、独立绑卡、特殊业务、回归共五个测试维度。

## 测试维度组织

测试用例集按 Sheet 组织，分为以下 5 个维度：

- Old Cashier（老收银台）
- New Cashier（新收银台）
- Standalone Binding（独立绑卡）
- Special Business（特殊业务）
- Regression（回归）

## Old Cashier（老收银台）

老收银台测试场景，按以下模块组织：

- Prerequisites（前置条件）
- Category（分类）
- Normal flow（正常流程）
- Exception flow（异常流程）
- Payment auth + risk rules（支付鉴权 + 风控规则）

## New Cashier（新收银台）

新收银台测试场景，按以下模块组织：

- Prerequisites（前置条件）
- Category（分类）
- Standard cashier（标准收银台）
- Exception flow（异常流程）

老/新收银台具体测试卡用例参见 [[scn_cko_subscription_test_cases]]。

## Standalone Binding（独立绑卡）

独立绑卡测试场景，按以下模块组织：

- Prerequisites（前置条件）
- Category — Case No.（分类与用例编号）
- Standalone binding（独立绑卡），用例编号 1–7

每个用例对应 Card contract info linked to Card_id 中的一条记录（Case No. 1 至 7）。详见 [[scn_cko_standalone_card_binding]]。

## Special Business（特殊业务）

特殊业务测试场景，按以下模块组织：

- Prerequisites（前置条件）
- Category（分类）
- Special business (normal)（特殊业务-正常）

## Regression（回归）

回归测试场景，按以下模块组织：

- Prerequisites（前置条件）
- Category（分类）
- Regression（回归）

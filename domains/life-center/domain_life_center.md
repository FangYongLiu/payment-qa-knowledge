---
id: domain_life_center
object_type: Domain
domain: life-center
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-20'
source_type: wiki
source_ref: confluence:PMDPayment/843841543
tags:
- mobile-topup
- life-service
subdomain: null
module: null
sensitivity: normal
name: Life Center 业务域
aliases: []
related_services: []
related_tables: []
related_scenarios:
- life-center-sgs-api-overview
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
Life Center 业务域属于生活服务类业务范畴，本文档范围内聚焦于 Mobile Top-up（话费充值/账单）相关的 SGS API 流程。

## 覆盖范围
当前文档涵盖的 Life Center 业务能力包括：
- Mobile Top-up（话费充值与账单查询）
  - Query prepaid international（查询国际预付话费）
  - Query prepaid mobile Top-up（查询本地预付话费充值）
  - Query postpaid mobile bill（查询后付费话费账单）
  - Place mobile order - Prepaid（预付话费下单）

## 关键服务/流程
本业务域在文档中以 SGS API 形式对外提供能力，关键流程节点：
- 查询类：Query prepaid international、Query prepaid mobile Top-up、Query postpaid mobile bill
- 交易类：Place mobile order - Prepaid

## QA 关注点
- 验证 Mobile Top-up 各查询接口与下单接口之间的数据/状态衔接是否一致。
- 区分 Prepaid（预付）与 Postpaid（后付）两类业务流程的处理路径。
- 区分国际（international）与本地（mobile Top-up）预付查询的差异点。
- 文档原文以流程图形式呈现（image-20241203-095941 等），具体字段、错误码、状态需结合各 API 子对象核对，本对象不展开。

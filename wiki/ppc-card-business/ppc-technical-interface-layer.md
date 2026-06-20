---
title: PPC技术接口层总览
domain: ppc-card-business
kind: wiki_page
slug: ppc-technical-interface-layer
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2135392298
tags: []
---

# PPC技术接口层总览

本页规划 PPC 卡业务"技术接口层"的内容范围，用于约束接口字段、数据库表结构与上下游依赖，使 LLM 能基于接口契约生成可执行的接口/集成测试用例。

## 本层用途

- 决定测试用例的"形态"：接口字段、数据库表结构、上下游依赖
- 为 LLM 提供接口契约，支撑接口测试与集成测试用例生成

## 核心 API 清单

覆盖卡片全生命周期与交易类操作：

- 开卡
- 激活
- 查余额
- 查交易
- 冻结 / 解冻
- 挂失
- 补卡
- 销卡
- 换 PIN
- 查 CVV
- 3DS 验证

## 卡组织接口

- Mastercard MCAPI
- Jaywan 接口
- Sandbox 域名 / 证书

## 异步事件

- 授权报文
- 清算文件
- 退款回执
- 风控决策回调

## 关键表与字段

重点关注金额、状态、币种字段：

- `card`
- `card_account`
- `card_authorization`
- `card_clearing`
- `card_transaction`
- `card_dispute`

## 上下游依赖

依赖图涉及以下系统/服务：

- KYC
- 风控
- 账务
- 清结算
- 通知中心
- 汇率服务

## 数据来源

- 接口文档（apidoc / Yapi）
- 数据库 DDL
- 系统架构图（Confluence Pay Core Workspace）
- 接口联调文档

## 维护责任

- 主负责人：Jianfei Wang
- 内容贡献：建议每个接口由对应 owner 维护
- 状态：骨架（待补充）
- 子页：见左侧页面树

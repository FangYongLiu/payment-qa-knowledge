---
title: MCC 测试集
domain: ppc-card-business
kind: wiki_page
slug: ppc-mcc-test-set
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2133819527
tags: []
---

# MCC 测试集

> 状态：骨架（待补充）

PPC 卡业务的 MCC（商户类别码）测试样本库。MCC 直接影响消费可达性、限额、风控与合规，是 PPC 用例设计中的关键变量。

## 用途

- 维护 MCC 测试样本，覆盖 PPC 卡用例中需验证的商户类别场景。
- 服务于限额、风控、合规及白/黑名单等相关测试。

## 记录字段结构

每个 MCC 作为一条记录，字段如下：

| 字段 | 说明 |
|---|---|
| MCC 编码 | 4 位数字 |
| 业务名 | 中英文 |
| 分类 | 白名单 / 黑名单 / 高风险 / 普通 |
| 适用卡产品 | 哪些卡可消费 |
| 限额特殊配置 | 与默认限额的差异 |
| 风控规则 | 是否触发额外审核 |
| 合规要求 | 监管对该 MCC 的特殊要求（如博彩、加密货币） |
| 测试 Sandbox 是否支持 | ✅/❌ |

## 覆盖建议

至少各取 1 个，覆盖以下类别：

- 白名单
- 黑名单
- 高风险：博彩、加密货币、成人
- 普通超市
- 餐饮
- 加油
- ATM 取现
- 跨境

此外，必须包含监管特别关注的 MCC（如 UAE 监管禁止的）。

## 数据来源

- 卡组织 MCC 编码表（Mastercard / Jaywan）
- 内部 MCC 配置
- 监管文件中的禁止/限制 MCC 清单

## 内容

待补充。

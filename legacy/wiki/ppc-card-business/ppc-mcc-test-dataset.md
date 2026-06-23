---
title: MCC 测试集
domain: ppc-card-business
kind: wiki_page
slug: ppc-mcc-test-dataset
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:f03ea93e-95b6-459e-9cf7-a78acdb5eec4
tags: []
---

# MCC 测试集

PPC 卡业务的 MCC（商户类别码）测试样本库，用于覆盖消费可达性、限额、风控、合规等关键测试维度。当前页面为骨架，待补充。

## 用途

MCC 是 PPC 用例的关键变量，直接影响：

- 消费可达性
- 限额
- 风控
- 合规

## 样本记录字段

每个 MCC 一条记录，包含以下字段：

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

## 覆盖范围建议

至少各取 1 个样本：

- 白名单
- 黑名单
- 高风险：博彩、加密货币、成人
- 普通超市
- 餐饮
- 加油
- ATM 取现
- 跨境

必含监管特别关注的 MCC（如 UAE 监管禁止的）。

## 数据来源

- 卡组织 MCC 编码表（Mastercard / Jaywan）
- 内部 MCC 配置
- 监管文件中的禁止/限制 MCC 清单

## 状态

内容待补充。

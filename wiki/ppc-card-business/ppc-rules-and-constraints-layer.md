---
title: PPC 规则与约束层总览
domain: ppc-card-business
kind: wiki_page
slug: ppc-rules-and-constraints-layer
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:9bb07775-b90e-47ab-8aeb-271e3bce8225
tags: []
---

# PPC 规则与约束层总览

PPC 业务定义中最复杂的一层，决定测试用例的"对错"判定标准——用例是否符合卡组织规则、监管合规、限额体系，以及是否踩中资损红线，均由本层裁定。

## 本层用途

- 为测试用例提供合规与风险维度的判定依据
- 覆盖四类核心约束：卡组织规则、监管合规、限额体系、资损红线

## 应包含的内容

### 卡组织规则差异
对比 Mastercard 与 Jaywan 在以下维度的差异：
- MCC
- Authorization Hold
- 清算时效
- 退款
- 退单

### 监管合规
- UAE Central Bank
- AML/CFT
- KYC 分级与额度上限
- 卡 BIN 备案

### 限额体系
- 时间维度：单笔 / 日 / 月 / 年
- 渠道维度：ATM / POS / 线上 / 跨境
- MCC 黑白名单
- 多币种合并计算口径

### 资损红线清单
必出测试用例的红线场景，包括但不限于：
- 双花
- 汇率精度
- 部分退款
- 强制入账

## 数据来源

- 卡组织规则文档：Mastercard MasterCom、Jaywan Operating Rules
- UAE Central Bank Regulation（Prepaid Card / AML / KYC）
- 内部限额配置文档
- 历史资损事故复盘

## 维护责任

| 角色 | 责任人 |
|---|---|
| 主负责人 | Jianfei Wang |
| 合规审核 | 待指定（建议合规/法务参与） |
| 内容贡献 | 待指定 |

## 状态

骨架（待补充），创建于 2026-05-04。具体子页见左侧页面树。

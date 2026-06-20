---
title: PPC规则与约束层总览
domain: ppc-card-business
kind: wiki_page
slug: ppc-rules-and-constraints-layer
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2133884995
tags: []
---

# PPC规则与约束层总览

> 创建于 2026-05-04 ｜ 维护人：Jianfei Wang ｜ 状态：骨架（待补充）

PPC 最复杂的一层。决定测试用例的"对错"——一个用例符不符合卡组织规则、监管合规、限额体系、是否踩资损红线，全在这一层判定。

## 本层用途

- 作为测试用例正确性的**判定基准**
- 覆盖卡组织规则、监管合规、限额体系、资损红线四个维度
- 任一用例的预期结果都需追溯到本层的某条规则

## 内容范围

### 卡组织规则差异
Mastercard 与 Jaywan 在以下方面的差异：
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
- 单笔 / 日 / 月 / 年
- ATM / POS / 线上 / 跨境
- MCC 黑白名单
- 多币种合并计算口径

### 资损红线清单
必出测试用例的红线场景：
- 双花
- 汇率精度
- 部分退款
- 强制入账
- 等

## 数据来源

- 卡组织规则文档（Mastercard MasterCom、Jaywan Operating Rules）
- UAE Central Bank Regulation（Prepaid Card / AML / KYC）
- 内部限额配置文档
- 历史资损事故复盘

## 维护责任

| 角色 | 责任人 |
|---|---|
| 主负责人 | Jianfei Wang |
| 合规审核 | 待指定（建议合规/法务参与） |
| 内容贡献 | 待指定 |

## 子页

见左侧页面树。

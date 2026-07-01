---
title: 知识库约定：业务域 owner 字段语义
domain: bimo-confirmed
kind: wiki_page
slug: kb-conventions-owner-field
status: active
owner: qa@example.com
reviewer: UNREVIEWED
source_type: conversation
source_ref: bimoqa-conversation:f3c0bc4b48f5
tags: []
---

# 知识库约定：业务域 owner 字段语义

本页明确知识库中各业务域 `owner` 字段的语义约定，避免与"产品/业务负责人"产生混淆。

## 约定

- 知识库中各业务域条目里的 `owner` 字段，统一指 **QA 负责人**。
- 不指代产品负责人，也不指代业务负责人。

## 示例

- KYC 域的 `owner` = **xinwei.cao**，即 KYC 的 QA 负责人。

## 适用范围

- 该约定适用于知识库中所有业务域条目，不限于单一域。
- 后续查人、分派测试责任时，均以此约定解释 `owner` 字段。

## 备注

- 此前曾存在将 `owner` 误解为"产品/业务 owner"的情况，特此记入知识库以统一口径。

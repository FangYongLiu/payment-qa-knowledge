---
title: Merchant Portal 商户入驻流程
domain: authorization-protocol
kind: wiki_page
slug: merchant-portal-onboarding
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:de47a1b0-67b1-48c9-ac4c-ff5b903e1d03
tags: []
---

# Merchant Portal 商户入驻流程

本页描述商户在 Botim Money Business Merchant Portal 完成 KYB 入驻的三步流程，并给出第一步 Company Profile 表单的字段清单。

## 入驻流程总览

商户控台采用 3 步 KYB 入驻流程，进度条按以下顺序推进：

1. **Company Profile**（公司资料，当前步骤）
2. **Company Credentials**（公司证件）
3. **Management**（管理层信息）

完成当前页表单并点击 **Continue** 后进入下一步 Company Credentials；表单底部同时提供 **Save Draft** 用于暂存草稿。

## Company Profile 表单

第一步表单分为 Company Profile 与 Registered Address 两个区块，标注 `*` 的字段为必填。

### Company Profile 区块

| 字段 | 必填 | 控件 / 说明 |
|---|---|---|
| Company name | 是 | 文本输入，需与 trade license 一致（According to the trade license） |
| Company website | 否 | 文本输入 |
| Industry | 是 | 下拉选择 |
| High-Risk Jurisdiction Involvement | 是 | 下拉选择（Choose areas of your business） |
| Monthly Turnover | 是 | 下拉选择 |
| Payment Method Accepted | 是 | 下拉选择（Choose payment method） |

### Registered Address 区块

该区块对应 trade license 上登记的注册地址（The address registered on the trade license）。

| 字段 | 必填 | 控件 / 说明 |
|---|---|---|
| Company number | 是 | 带国家区号的电话输入，默认 `+971` |
| Email address | 是 | 文本输入 |
| Country | 是 | 下拉选择，默认 `United Arab Emirates` |
| Emirates | 是 | 下拉选择城市 |
| Area | 是 | 文本输入 |
| Building Name | 是 | 文本输入 |
| Office No. | 是 | 文本输入 |
| Are registered address and company address the same? | 是 | 选择控件 |

## 底部操作

- **Save Draft**：保存为草稿，便于后续继续填写。
- **Continue**：校验通过后进入第 2 步 Company Credentials。

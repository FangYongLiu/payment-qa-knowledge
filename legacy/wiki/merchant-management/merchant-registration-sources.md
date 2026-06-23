---
title: 商户注册来源概览
domain: merchant-management
kind: wiki_page
slug: merchant-registration-sources
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:3f924dac-6ff7-4ef2-8427-4cac5a6ac24d
tags: []
---

# 商户注册来源概览

本页基于 Standard POS Guide 中的入驻 UI，整理商户注册（KYC）表单中需要填写与上传的字段，用于 UAE 地区 Standard POS 商户的合规登记。

## 表单标题

- 页面提示语：**Please fill in the merchant information**
- 用途：KYC / 商户注册，采集贸易执照、法律实体信息、营业地址以及身份/公司章程类文件。

## 必填字段（带 `*`）

### 商户基本信息

- **Merchant Name (As per trade license)**：文本输入，须与贸易执照一致
- **Category**：下拉选择（占位 `Choose Category`）
- **Legal Status**：下拉选择（占位 `Choose Legal Status`）

### 贸易执照

- **Trade License**：文件上传
- **Trade License Expiry Date**：日期输入，格式 `DD/MM/YYYY`
- **Trade License No**：文本输入

### 营业地址

- **Country/Region**：下拉，默认值 `United Arab Emirates`
- **Emirates/City**：下拉选择（占位 `Choose Emirate`）
- **Registered Business Address**：文本输入

### 身份证件上传

字段名：**Owner's VALID Emirates ID or Passport copy**，提供两个上传框：

- 第一框（必填）：`Front & Back copy for Owner/Partner/POA 1`
- 第二框（可选）：`Front & Back copy for Owner/Partner/POA 2 (if any)`

## 可选字段

- **Articles/Memorandum Of Association**：公司章程/组织大纲文件上传（非必填）

## 适用范围

- 产品线：Standard POS
- 地区：United Arab Emirates（默认国家已预填）
- 场景：商户首次入驻时的 KYC 信息采集

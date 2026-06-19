---
title: Merchant Portal 管理员信息表单截图
domain: authorization-protocol
kind: wiki_page
slug: merchant-portal-admin-info-screenshot
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:2e6165f4-d264-4bdb-9680-33fd461b9bca
tags: []
---

# Merchant Portal 管理员信息表单截图

本页说明 Botim Money Business 商户控台注册流程中 **Administrator Information**（管理员信息）部分的表单字段、上传项与示例填写内容。

## 页面位置与上下文

- 页面顶部展示 `botim MONEY BUSINESS` Logo。
- Administrator Information 区块上方为一个文件上传 dropzone（部分可见），提示文案：
  - `Drag and drop the file or upload a file`
  - `Accepts JPG,PNG, and PDF files | Max file size : 5mb`

## Administrator Information 表单字段

区块标题：**Administrator Information**。表单为两列布局，所有字段均为必填（标记 `*`）。

- 左列：
  - `Type administrator name or choose a partner/signatory *` — 示例值：`fangyong`
  - `Mobile number *` — 国家码下拉 `+971`，号码 `556579167`
- 右列：
  - `Email address *` — 示例值：`liufangyong168@gmail.com`
  - `Designation *` — 示例值：`fangyong`

## 证件类型选择

字段：`Select the document type`，提供两个单选项：

- `Emirates ID`（已选中）
- `Passport`（未选中）

## 证件与授权文件上传

- `Emirates ID (Front) *` — 已上传文件，显示为 PDF 图标，文件名 `1772113291376.jpg`，附红色删除（trash）图标。
- `Emirates ID (Back) *` — 已上传文件 `1772113294176.jpg`，附删除图标。
- `Letter of authorization *` — 空 dropzone，提示文案 `Drag and drop the file or upload a file / Accepts JPG,PNG, and PDF files | Max file size : 5mb`。
  - 辅助说明（下方）：`Download the Letter of Authorization template to fill it, and then re-upload it.`，其中 `Download` 为绿色超链接，用于下载授权书模板。

## 证件信息字段

- `Emirates ID Number *` — 示例值：`784-9714-8794579-4`
- `Expiry date *` — 日期输入框，示例值 `01-03-2029`，附日历图标。

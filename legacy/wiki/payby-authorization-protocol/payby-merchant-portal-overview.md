---
title: PayBy Merchant Portal(商户控台)概览
domain: authorization-protocol
kind: wiki_page
slug: payby-merchant-portal-overview
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:22afbc40-24fe-4c96-b4d7-d33acacdeb9c
tags: []
---

# PayBy Merchant Portal(商户控台)概览

本页介绍 PayBy Merchant Portal 商户入驻注册表单中的字段与上传项，覆盖文件上传规范、管理员信息、证件类型与编号等内容。

## 文件上传规范

- 上传方式：拖拽文件或点击 `upload a file` 链接上传
- 支持格式：JPG、PNG、PDF
- 单文件大小上限：5mb
- 已上传文件以文件名 chip 形式展示，可通过红色删除图标移除

## 银行流水上传

- 字段：`Bank statement for the last 3 months`
- 上传方式与限制同上(JPG/PNG/PDF，≤5mb)

## Administrator Information(管理员信息)

注册表单中的管理员信息分区，包含以下必填字段：

- `Type administrator name or choose a partner/signatory *`：管理员姓名，或选择合伙人/签署人
- `Email address *`：邮箱地址
- `Mobile number *`：手机号，含国家区号下拉(示例 `+971`) + 号码输入
- `Designation *`：职位/职务

## 证件类型与上传

`Select the document type` 提供两种证件类型(单选)：

- `Emirates ID`(默认选中)
- `Passport`

### 选择 Emirates ID 时需提交的材料

- `Emirates ID (Front) *`：身份证正面照片
- `Emirates ID (Back) *`：身份证背面照片
- `Letter of authorization *`：授权书
- `Emirates ID Number *`：身份证号(示例格式 `784-9714-8794579-4`)

以上文件上传项均遵循统一的格式与大小限制(JPG/PNG/PDF，≤5mb)。

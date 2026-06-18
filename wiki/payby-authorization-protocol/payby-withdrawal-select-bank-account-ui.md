---
title: 提现-选择银行账户页面UI说明
domain: payby-authorization-protocol
kind: wiki_page
slug: payby-withdrawal-select-bank-account-ui
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:14053595-40d1-4be0-be35-ec8cece6d132
tags: []
---

# 提现-选择银行账户页面UI说明

本页描述提现流程中"Select Bank Account（选择银行账户）"页面的界面元素与交互行为。

## 页面概览

- 平台：移动端（iOS）
- 场景：提现流程中选择提现目标银行账户
- 页面标题：Select Bank Account

## 顶部导航栏

- 左侧：返回箭头（back arrow），用于回到上一页
- 中间：页面标题 `Select Bank Account`

## 银行账户列表项

页面主体为银行账户列表，每一行代表一个可选的银行账户。示例项包含以下元素：

- 银行 Logo：圆形头像，显示银行标识 `FAB`，副标 `First Abu Dhabi Bank`，并带有红色对勾标记
- 账户昵称（Label/nickname）：灰色文字，例如 `我们`
- 脱敏账号：仅显示尾号，例如 `******************1010`
- 银行名称：完整银行名称，例如 `First Abu Dhabi Bank PJSC`

## 交互说明

- 用户点击某一行账户项，即可将该银行账户选定为本次提现的收款目标
- 当用户仅绑定一个银行账户时，列表中只显示一条记录，页面其余区域为白色空白背景

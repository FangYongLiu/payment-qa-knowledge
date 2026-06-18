---
title: 商户控台登录页面说明
domain: payby-authorization-protocol
kind: wiki_page
slug: merchant-portal-login-screen
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:1f405e46-7cdf-4bf1-8c73-31341821eee2
tags: []
---

# 商户控台登录页面说明

本页描述 Botim Money Business 商户控台的登录/注册入口页面 UI 元素与交互流程。

## 页面定位

- 产品名称：**Botim Money Business**（商户控台 Merchant Portal）
- 页面类型：登录 / 注册统一入口
- 入口方式：基于手机号的单步认证

## 品牌标识区

页面顶部居中展示品牌 Logo：

- `botim` 字样（黑色，"b" 字母带绿色圆点点缀）
- 黑色胶囊徽章内显示绿色 `MONEY` 字样
- 下方白色小徽章显示黑色 `BUSINESS` 字样

## 登录表单

白色圆角卡片承载登录表单，包含以下元素：

- **标题**：`Welcome`（大号粗体，深灰色）
- **手机号输入行**：
  - 国家码选择器：默认显示 `+971`（阿联酋），带下拉箭头 `▾`
  - 手机号输入框：占位符为 `Phone Number`
- **主操作按钮**：全宽绿色按钮，白色文字 `Sign in/Sign Up`

## 交互流程

- 单步入口：商户用户输入手机号后点击 `Sign in/Sign Up` 按钮即可提交。
- 登录与注册合一：同一按钮同时处理 **新用户注册** 与 **老用户登录** 两种场景。
- 默认国家码：`+971`（UAE），可通过下拉切换。
- 后续流程：提交后预期进入 OTP 验证流程（基于手机号的一次性验证码认证）。

## 视觉风格

- 背景：浅灰色，右下角与右上角带有淡灰色斜向几何线条装饰。
- 卡片：白色圆角容器，居中布局。
- 主色调：绿色（品牌色，用于强调点缀与主按钮）。

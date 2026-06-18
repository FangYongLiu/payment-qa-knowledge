---
title: Merchant Portal 商户控台
domain: payby-authorization-protocol
kind: wiki_page
slug: merchant-portal-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:89183b89-c001-4cdf-9711-f201c5bc8f44
tags: []
---

# Merchant Portal 商户控台

Botim Money Business 商户控台的登录入口页面，商户通过手机号统一完成注册与登录。

## 登录入口

- 站点品牌标识：`botim` + `MONEY` + `BUSINESS`（商户业务版）
- 登录方式：手机号登录/注册一体化
- 默认国家区号：`+971`（阿联酋），支持下拉切换

## 登录表单字段

| 元素 | 说明 |
|------|------|
| 区号选择器 | 默认 `+971`，可下拉切换其他国家区号 |
| Phone Number | 手机号输入框 |
| Sign in/Sign Up | 主操作按钮，同一按钮同时承载首次注册与老用户登录两种场景 |

## 交互流程

- 商户在登录页输入手机号并点击 `Sign in/Sign Up`
- 系统根据手机号判断是新注册还是已有账户登录
- 后续进入基于手机号的 OTP 验证流程完成身份认证

## 页面说明

- 标题文案：`Welcome`
- 单步入口设计：无需在登录前区分"注册"或"登录"路径，由后端按手机号自动路由

</br>

![Merchant Portal 登录页](image-20260226-133013.png)

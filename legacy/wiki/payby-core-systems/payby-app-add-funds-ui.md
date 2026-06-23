---
title: PayBy App 充值页面UI说明
domain: payby-core-systems
kind: wiki_page
slug: payby-app-add-funds-ui
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:cfaf8167-d8cd-485b-9212-70b3441cab80
tags: []
---

# PayBy App 充值页面UI说明

本页描述钱包 App "Add funds"（充值）页面的 UI 元素、交互流程及 QA 关注点。

## 页面用途

- 所属流程：支付/钱包 App 的 **Add funds** 充值流程
- 用户在此页查看当前钱包余额，输入或选择充值金额，进入下一步（推测为支付方式选择/确认）

## 顶部区域

- 左上：返回箭头（Back）
- 右上：**Deposit cash** 链接（蓝色），用作另一种充值入口
- 页面标题：**Add funds**

## 余额展示

- 文案：`Balance: 863.62 AED`
- 右侧：信息图标 (i)，可查看余额相关说明

## 金额输入区

- 浅灰圆角容器卡片
- 币种符号：`₿`（类似 BHD 字形）+ 已输入金额 `1`
- 快捷金额 pill 按钮（预设档位）：
  - `100`
  - `200`
  - `500`
  - `1000`

## 辅助链接

- 输入卡片下方：**View limit** 链接（蓝色），用于查看充值限额

## 主 CTA

- 底部全宽蓝色圆角按钮：**Proceed to add funds**（带右箭头）
- 点击后进入下一步流程

## 交互流程

1. 用户进入页面，查看当前余额（`863.62 AED`）
2. 通过输入框手动输入金额，或点击预设档位（100/200/500/1000）
3. 可选：
   - 点 **View limit** 查看限额
   - 点 **Deposit cash** 切换至现金充值入口
4. 点击 **Proceed to add funds** 进入后续步骤

## QA 注意点

- **币种显示一致性**：
  - 余额显示币种为 `AED`
  - 金额输入框币种符号显示为 `₿`（疑似 BHD 字形）
  - 二者不一致，可能为显示异常，需重点验证币种渲染逻辑与符号映射

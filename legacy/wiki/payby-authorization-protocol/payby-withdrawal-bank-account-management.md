---
title: PayBy提现-银行账户管理
domain: authorization-protocol
kind: wiki_page
slug: payby-withdrawal-bank-account-management
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:be02e4fc-16b4-4ab4-b8fa-c4c50da300c9
tags: []
---

# PayBy提现-银行账户管理

提现流程中，用户在 **Select Bank Account** 页面查看已绑定的银行账户列表，并可对单个账户发起删除操作，删除前需通过弹窗二次确认。

## 银行账户列表页

- 页面标题：**Select Bank Account**
- 顶部左侧提供返回箭头，可退出选择页
- 列表项展示内容：
  - 银行 Logo（圆形图标）
  - 账户标签（如 `我们`）
  - 脱敏账号（仅显示尾号，例如 `*******************1010`）
  - 开户行名称（如 `First Abu Dhabi Bank PJSC`）

## 删除确认弹窗

用户在列表中触发删除操作后，弹出居中的白色圆角确认对话框：

- 提示文案：**Do you want to delete this account?**
- 操作按钮（由分隔线分开）：
  - **Cancel**（左侧，灰色文字）：关闭弹窗，返回账户列表，不做任何变更
  - **Confirm**（右侧，黑色加粗文字）：确认删除当前选中的银行账户（如尾号 `1010` 的 FAB 账户）

---
title: PayBy提现-银行转账支付确认页UI
domain: payby-withdrawal
kind: wiki_page
slug: payby-withdrawal-confirm-ui
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:58ea64a7-4246-42fa-aa76-9d1a3f0c36df
tags: []
---

# PayBy提现-银行转账支付确认页UI

本页描述 PayBy 提现至银行账户流程中，"Confirm Your Payment" 支付确认弹窗的 UI 构成与金额计算关系。

## 入口页面（背景页）

提现确认弹窗由 "Transfer to Bank Account" 页面唤起，背景页元素：

- 顶部标题：`Transfer to Bank Account`
- 左侧返回箭头
- 右上角入口：`History`（绿色链接）
- 字段：
  - `Account holder name`：收款人姓名（右侧带联系人/地址簿图标）
  - `IBAN`：以掩码形式展示，仅显示后 4 位（示例 `******************1010`）

## 支付确认弹窗（Confirm Your Payment）

底部弹出的白色 bottom-sheet 模态框，用于二次确认本次提现支付。

- 左上角：关闭按钮 `X`
- 标题：`Confirm Your Payment`（居中）
- 主显示金额：大字号展示**总扣款金额**（示例 `AED 3.00`）
- 底部主按钮：绿色 `CONFIRM`

## 明细字段

弹窗内自上而下展示以下明细行：

| 字段 | 含义 | 示例 |
| --- | --- | --- |
| `Order Info` | 订单类型说明 | `Transfer to Bank Account` |
| `Amount` | 提现金额（到账金额） | `AED 1.00` |
| `Fees` | 手续费（置灰展示） | `AED 2.00` |
| `Payment Method` | 支付方式（带硬币图标） | `Balance` |

## 金额构成关系

弹窗顶部展示的大额金额为本次实际扣款总额，构成关系为：

```
顶部展示金额 = Amount + Fees
AED 3.00    = AED 1.00 (到账) + AED 2.00 (手续费)
```

- 资金来源：用户的 `Balance`（余额）
- 资金去向：背景页所示 IBAN 对应的银行账户（持卡人为 `Account holder name`）

## 交互流程

1. 用户在 `Transfer to Bank Account` 页填写收款人与 IBAN 后发起提现
2. 弹出 `Confirm Your Payment` 确认弹窗，展示总扣款额与明细
3. 点击 `CONFIRM` 执行扣款并发起银行转账；点击 `X` 取消本次操作

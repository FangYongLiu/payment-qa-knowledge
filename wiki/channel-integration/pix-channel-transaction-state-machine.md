---
title: PIX渠道交易状态机
domain: channel-integration
kind: wiki_page
slug: pix-channel-transaction-state-machine
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:3ecee441-5c2f-476e-9f2a-a1f9f61b97ed
tags: []
---

# PIX渠道交易状态机

本页描述 PIX 渠道支付交易的完整生命周期，涵盖从交易初始化到终态（成功通知 / 关闭 / 撤销）的状态流转。

## 状态列表

- **P-Processing**：交易处理中（入口状态）
- **PS-PaySuccess**：收银台支付成功
- **NS-NotifySuccess**：通知支付成功（成功终态）
- **C-Closed**：交易关闭（终态）
- **PC-PayCancel**：支付撤销（终态）

## 状态流转

### 初始化

- 初始伪状态 → `trade initialized` → **P-Processing**

### P-Processing 出向

- `cashier paid` → **PS-PaySuccess**
- `trade closed or transaction failed` → **C-Closed**

### PS-PaySuccess 出向

- `notify payment success` → **NS-NotifySuccess**
- `transaction failed` → **PC-PayCancel**

### C-Closed 出向

- `cashier paid` → **PC-PayCancel**（交易已关闭后发生的迟到支付）
- → 终态

### NS-NotifySuccess 出向

- → 终态

### PC-PayCancel 出向

- → 终态

## 关键路径

- **成功路径**：P-Processing → PS-PaySuccess → NS-NotifySuccess
- **关闭路径**：P-Processing → C-Closed
- **撤销路径**（两条进入 PC-PayCancel 的路径）：
  - PS-PaySuccess 经 `transaction failed` → PC-PayCancel
  - C-Closed 经 `cashier paid` → PC-PayCancel（关单后迟到付款触发撤销）

## 终态

共三个终态出口：

- NS-NotifySuccess 之后（成功）
- C-Closed 之后（关闭）
- PC-PayCancel 之后（撤销）

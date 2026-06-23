---
title: 提现到银行账户表单界面说明
domain: withdraw-cash
kind: wiki_page
slug: payby-withdrawal-transfer-to-bank-ui
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:cd7c12ea-901f-482a-8406-c9d9813f5867
tags: []
---

# 提现到银行账户表单界面说明

本页描述 PayBy 提现流程中"Transfer to Bank Account"（提现到银行账户）表单页的 UI 结构、字段交互与跳转入口。

## 页面顶部导航

- 左侧：返回箭头
- 中间标题：**Transfer to Bank Account**
- 右上角：**History** 链接（绿色），用于查看历史转账记录

## 表单字段

按从上到下顺序排列：

1. **Account holder name**（收款人姓名）
   - 占位符：`Please enter holder name`
   - 右侧附带绿色通讯录图标，下方标注 **Beneficiary**，点击可从已保存的收款人列表中选择
   - 当前为聚焦/激活状态（绿色下划线）
2. **IBAN**
   - 占位符：`Please enter IBAN No.`
   - 灰色下划线
3. **Bank name**（银行名称）
   - 空输入框，灰色下划线
   - 通常由 IBAN 自动解析填充
4. **Amount**（金额）
   - 占位符：`Amount`
   - 灰色下划线

## 金额辅助信息

位于 Amount 字段下方：

- 第一行：`Balance:AED152.00,` 后接绿色链接 **Transfer All**（一键填入全部余额）
- 第二行：`View` 后接绿色链接 **Price Plan**（查看费率/价格方案）

## 主操作按钮

- 底部为大号绿色矩形 CTA 按钮，白色大写文字 **NEXT**
- 点击后进入提现流程的下一步

## 交互流转

用户填写收款人姓名（或通过 Beneficiary 选择已保存收款人）→ 输入 IBAN → Bank name 自动解析 → 输入 Amount（受余额 AED 152.00 限制，可用 Transfer All 快捷填入）→ 点击 NEXT 进入下一步。

辅助入口：

- **History**：查看历史转账记录
- **Price Plan**：查看手续费规则

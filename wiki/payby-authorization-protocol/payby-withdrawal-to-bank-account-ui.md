---
title: 提现到银行账户界面说明
domain: authorization-protocol
kind: wiki_page
slug: payby-withdrawal-to-bank-account-ui
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:cc3cdfb0-78ba-4e27-99b6-db73723a0a2c
tags: []
---

# 提现到银行账户界面说明

本页描述 PayBy 钱包"提现到银行账户"（Transfer to Bank Account）页面的 UI 布局、输入字段与交互入口。

## 页面布局

页面为移动端单页表单，自上而下分为顶部导航栏、表单字段区与底部操作按钮。

## 顶部导航栏

- 左侧：返回箭头
- 中间：标题 **Transfer to Bank Account**
- 右侧：**History** 链接，跳转至历史转账记录

## 表单字段

按从上到下顺序排列：

1. **Account holder name**（账户持有人姓名）
   - 示例值：`SHUNXIANG LIN`
   - 输入框右侧显示绿色勾选图标，表示校验通过
2. **IBAN**
   - 占位提示：`Please enter IBAN No.`
3. **Bank name**（银行名称）
   - 输入框为空
4. **Amount(AED)**（提现金额，单位 AED）
   - 占位提示：`Amount`
   - 下方辅助文案：`Balance AED 21.34  Transfer All`
     - `Transfer All` 为操作链接，点击后将可用余额自动填入金额输入框
   - 再下方：`View Price Plan` 链接，用于查看费率/价格方案

## 底部操作

- 全宽绿色主按钮：**NEXT**
- 点击后进入提现流程的下一步

## 交互流程

1. 用户填写收款人银行信息：持有人姓名、IBAN、银行名称
2. 输入提现金额（AED），可选择 `Transfer All` 一键填入全部可用余额
3. 可通过 `View Price Plan` 查看手续费说明
4. 点击 **NEXT** 进入提现下一步骤
5. 通过右上角 **History** 可查看历史提现记录

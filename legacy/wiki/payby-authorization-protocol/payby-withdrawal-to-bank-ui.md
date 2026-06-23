---
title: PayBy提现至银行账户UI说明
domain: authorization-protocol
kind: wiki_page
slug: payby-withdrawal-to-bank-ui
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:e9727228-b765-4db4-bc6e-0eaaf3fcffc0
tags: []
---

# PayBy提现至银行账户UI说明

本页描述 PayBy "Transfer to Bank Account"（提现至银行账户）页面的表单字段、辅助交互与主操作按钮。

## 页面结构

- 顶部导航栏
  - 左侧：返回箭头
  - 居中标题：**Transfer to Bank Account**
  - 右侧：**History**（绿色文字链接，进入历史记录）
- 主体：提现表单
- 底部：主 CTA 按钮

## 表单字段

按从上到下顺序：

1. **Account holder name**（收款人姓名）
   - 预填当前用户姓名（示例：`SHUNXIANG LIN`）
   - 右侧绿色通讯录/联系人图标，提示可从联系人中选择
2. **IBAN**
   - 空输入框，占位文案：`Please enter IBAN No.`
3. **Bank name**（银行名称）
   - 默认空白，预期由 IBAN 自动解析回填
4. **Amount(AED)**（提现金额，币种 AED 阿联酋迪拉姆）
   - 空输入框，占位文案：`Amount`
   - 输入框下方显示当前余额：`Balance:AED 21.34`（灰色）
   - 余额右侧绿色快捷链接：**Transfer All**（一键全部提现）

## 辅助信息

- **View Price Plan**
  - `View` 灰色文字 + `Price Plan` 绿色链接
  - 用于查看费率/价格计划

## 主操作按钮（CTA）

- 页面底部通栏绿色按钮：**NEXT**（白色大写文字）
- 点击后进入提现流程的下一步

## 交互流程

1. 选择或编辑收款人姓名（可通过联系人图标选取）
2. 输入 IBAN，由系统解析并回填 Bank name
3. 输入提现金额（AED），金额上限受 Balance 约束；可点击 Transfer All 一键填入全部余额
4. 可选：点击 View Price Plan 查看费率
5. 点击 **NEXT** 进入下一步

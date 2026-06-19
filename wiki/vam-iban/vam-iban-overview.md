---
title: VAM IBAN 虚拟账户总览
domain: vam-iban
kind: wiki_page
slug: vam-iban-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:3fca2a3f-f2de-4193-b613-7e002319a335
tags: []
---

# VAM IBAN 虚拟账户总览

本页汇总 PayBy App 中 VAM IBAN 虚拟账户的申请激活入口、VIP 用户处理、批次 Job 重试机制、mock 配置以及交易通知测试方式。详细场景见 [[scn_vam_iban_apply_activate]]、[[scn_vam_iban_apply_and_transaction]] 与 [[scn_vam_iban_fitnesse_notify]]。

## 申请与激活入口

- 入口：PayBy App → 充值 → **Bank Account Transfer** → 点击激活
- 激活结果：
  - 激活成功：页面展示 IBAN 信息（PayBy Virtual Bank Account 详情页）
  - 激活处理中：等待批次 Job 重试处理
- 落库：写入 [[tbl_vis_t_virtual_account]]（通过 `mid` 关联），初始 `status=Initial`

## 虚拟账户详情页

激活成功后，App 进入 **PayBy Virtual Bank Account** 详情页：

- 顶部导航：返回 / 标题 `PayBy Virtual Bank Account` / 右上角 `FAQ`
- 卡片信息（PayBy × FAB 联合发行，FAB = First Abu Dhabi Bank / بنك أبوظبي الأول）：
  - `Account Holder`：账户持有人姓名
  - `VALID THRU`：有效期（示例 `05/23`）
  - `Account Type`：示例 `OTHER`
  - `Account No`：账户号（示例 `7415009140006171`），支持复制
  - `IBAN`：示例 `AE130357415009140006171`，支持复制
- 卡片下方：`Collection Record >` 入口
- **Receive** 区块，三个入口：
  1. `Salary`
  2. `Transactions`
  3. `International Transfer`

## VIP 用户处理

- VIP 用户点击 **Free Active** 按钮后，需补充姓名信息
- 姓名信息**无校验**

## 批次 Job 处理

- Job 名称：`vis_ibanAccountRetryJob`，详见 [[auto_vis_iban_account_retry_job]]
- 适用范围：除 **lean 场景** 外，其他 **fab 用户** 申请均走批次处理
- 触发动作：调用/打批发 fab，将 IBAN 数据状态更新为 `Valid`
- 库存不足场景：
  - 当 IBAN 无库存时，前端申请落库时不带 IBAN 信息
  - 处理方式：联系相关人员（如 wangqian）人工补充 IBAN 数据，等待 Job 重试

## Mock 配置

不调用 fab 的本地配置：

```yaml
vis:
  notification:
    mock: Y
```

## 交易通知测试

- 验证工具：Fitnesse
  - 入口路径：`http://fitnesse.test2pay.com/FrontPage.VisSuitePage.VisNotifyFacade.TestCaseN101`
  - 用途：模拟发送交易通知
- 落库表：[[tbl_vis_t_notify_transaction_flow]]

## 相关测试场景

- [[scn_vam_iban_apply_activate]]
- [[scn_vam_iban_apply_and_transaction]]
- [[scn_vam_iban_fitnesse_notify]]

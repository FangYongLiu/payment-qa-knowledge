---
title: VAM IBAN 虚拟账户总览
domain: vam-iban
kind: wiki_page
slug: vam-iban-overview
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:tester/219152444
tags: []
---

# VAM IBAN 虚拟账户总览

本页汇总 VAM IBAN 虚拟账户的申请激活入口、批次处理任务、mock 配置以及交易通知测试方式。详细场景见 [[scn_vam_iban_apply_activate]] 与 [[scn_vam_iban_fitnesse_notify]]。

## 申请与激活入口

- 入口：payby app 充值 → 选择 `Bank Account Transfer` → 点击激活
- 激活结果：
  - 成功：展示 iban 信息
  - 处理中：等待 job 重试
- VIP 用户：点击 `Free Active` 按钮后需补充姓名信息，无校验
- 落库：写入 [[tbl_vis_t_virtual_account]]（通过 `mid` 关联），初始 `status=Initial`

## 批次处理

- 除 lean 场景外，其他 fab 用户申请均走批次处理
- 任务：[[auto_vis_iban_account_retry_job]]（`vis_ibanAccountRetryJob`）
- 触发后调用 fab，将 iban 数据状态更新为 `Valid`
- 当 iban 无库存时，前端申请落库不带 iban 信息，可联系相关人员人工补 iban 数据后等 job 重试

## Mock 配置

不调用 fab 的本地配置：

```yaml
vis:
  notification:
    mock: Y
```

## 交易通知测试

- fitnesse 入口：`http://fitnesse.test2pay.com/FrontPage.VisSuitePage.VisNotifyFacade.TestCaseN101`
- 通过 fitnesse 模拟发交易通知
- 落库：[[tbl_vis_t_notify_transaction_flow]]

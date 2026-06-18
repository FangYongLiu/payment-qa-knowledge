---
title: VAM IBAN 申请与交易总览
domain: payby-authorization-protocol
kind: wiki_page
slug: vam-iban-overview
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:dc0d6822-f889-4a34-bdfe-72b5e0051862
tags: []
---

# VAM IBAN 申请与交易总览

本页介绍 PayBy App 中通过 Bank Account Transfer 入口申请激活 VAM IBAN 的完整流程、VIP 用户特殊处理、批次 Job 重试机制、mock 配置及交易通知验证方法。

## 申请 IBAN 流程

- 入口：PayBy App → 充值 → **Bank Account Transfer** → 点击激活
- 激活状态：
  - 激活成功：页面展示 IBAN 信息
  - 激活处理中：等待批次 Job 处理
- 落库：[[tbl_vis_t_virtual_account]]（通过 `mid` 关联），初始 `status=Initial`

## VIP 用户处理

- VIP 用户点击 **Free Active** 按钮后，需补充姓名信息
- 姓名信息**无校验**

## 批次 Job 处理

- Job 名称：`vis_ibanAccountRetryJob`，详见 [[auto_vis_iban_account_retry_job]]
- 适用范围：除 **lean 场景** 外，其他 **fab 用户** 申请均走批次处理
- 触发动作：打批发 fab，更新 IBAN 数据状态为 `Valid`
- 库存不足场景：
  - 前端申请落库时无 IBAN 信息
  - 处理方式：人工补充 IBAN 数据（联系 wangqian），等待 Job 重试

## Mock 配置

不调用 fab 的本地配置：

```yaml
vis:
  notification:
    mock: Y
```

## 交易通知验证

- 验证工具：Fitnesse
  - 路径：`http://fitnesse.test2pay.com/FrontPage.VisSuitePage.VisNotifyFacade.TestCaseN101`
  - 用途：模拟发送交易通知
- 落库表：[[tbl_vis_t_notify_transaction_flow]]

## 相关测试场景

- [[scn_vam_iban_apply_and_transaction]]

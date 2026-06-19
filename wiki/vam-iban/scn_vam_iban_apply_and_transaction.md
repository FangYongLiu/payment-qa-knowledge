---
title: VAM IBAN申请与交易测试场景
domain: vam-iban
kind: wiki_page
slug: scn_vam_iban_apply_and_transaction
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:251693c4-8d54-4faa-a417-bf7ddec20443
tags: []
---

# VAM IBAN申请与交易测试场景

## 触发/入口
- payby app 充值入口：选择 Bank Account Transfer → 点击激活（Free Active）
- fitness 入口模拟交易通知：http://fitnesse.test2pay.com/FrontPage.VisSuitePage.VisNotifyFacade.TestCaseN101

## 前置条件
- IBAN 库存充足；若库存为空，前端申请落库无 iban 信息，需人工补录 iban 数据后等待 job 重试
- Vip 用户点击 Free Active 后需补充姓名信息（无校验）
- mock 配置（不调用 fab）：
  ```
  vis:
    notification:
      mock: Y
  ```

## 操作步骤
1. 申请 IBAN：在 payby app 充值页选择 Bank Account Transfer，点击激活
   - 激活成功：展示 iban 信息
   - 激活处理中：进入批次处理
2. 批次处理：除 lean 场景外，其他 fab 用户申请都走批次处理，由 job `vis_ibanAccountRetryJob` 触发
   - job 触发后打批发 fab，更新 iban 数据状态
3. 配置 mock，避免实际调用 fab
4. 通过 fitness 用例 TestCaseN101 模拟发送交易通知

## 人工补录 IBAN 数据规范
当 IBAN 库存为空、需要人工补录时，参考导入表（含字段：Virtual Account Entity Identifier、Virtual Account ID、Virtual Account Name、Virtual Account IBAN、Virtual Account Type、Hierarchy Type），样例：
- Virtual Account Entity Identifier：40006
- Virtual Account ID：00000112
- Virtual Account Name：持有人姓名（如 MUHAMMAD TASHFEEN SAEED MALIK ...）
- Virtual Account IBAN：AE270357414000620231020
- Virtual Account Type：Payment and Collection
- Hierarchy Type：P

补录规则（重点字段）：
- **Virtual Account ID**：从末位开始修改，使其对应 `vis` 账户表里的 id。例如数据库 id=123，则把末尾 3 位 `112` 改为 `123`。⚠️ 切勿改变位数与格式。
- **Virtual Account IBAN**：必须保证唯一，建议使用日期后缀避免重复。

## DB 校验点
- `vis.t_virtual_account`（通过 mid 关联）
  - 申请激活后：status = Initial
  - job 处理后：status = Valid
- `vis.t_notify_transaction_flow`：交易通知后落库

## 预期结果
- IBAN 申请成功落库 `vis.t_virtual_account`，初始 status=Initial
- 经 `vis_ibanAccountRetryJob` 批次处理后，iban 状态更新为 Valid
- fitness 模拟交易通知后，交易流水落库 `vis.t_notify_transaction_flow`

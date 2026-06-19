---
title: VAM IBAN 申请与激活场景
domain: vam-iban
kind: wiki_page
slug: scn_vam_iban_apply_activate
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:bd12f410-6738-4a94-8a5d-6280c0cc6399
tags: []
---

# VAM IBAN 申请与激活场景

## 触发/入口
- PayBy App → 充值 → 选择 Bank Account Transfer → 直接点击激活
- VIP 用户：点击 Free Active 按钮（需补充姓名信息，无校验）

## 前置条件
- 用户登录 PayBy App，具备充值入口
- 区分用户类型：普通 fab 用户、VIP 用户、lean 场景用户
- IBAN 库存可用（无库存场景需人工介入）
- mock 配置（不调用 fab 时）：
  ```
  vis:
    notification:
      mock: Y
  ```

## 操作步骤
1. 进入充值页，选择 Bank Account Transfer
2. 点击激活按钮（VIP 用户为 Free Active，需补充姓名）
3. 前端展示三种状态之一：
   - 激活成功：展示 IBAN 信息
   - 激活处理中
   - 无 IBAN 信息（库存不足时）
4. 普通 fab 用户申请进入批次处理流程，由 job `vis_ibanAccountRetryJob` 处理
5. lean 场景不走批次处理（直接处理）
6. 无库存场景：可联系 wangqian 人工添加 IBAN 数据，等待 job 重试

## DB 校验点
- 表：`vis.t_virtual_account`（通过 mid 关联用户）
  - 申请落库后 `status=Initial`
  - job 批次处理调用 fab 成功后，`status=Valid`
- 无库存时落库记录无 IBAN 信息

## 人工补 IBAN 数据规范
当无库存需要人工添加 IBAN 时，按以下 Excel 模板字段提供数据：

| 列 | 字段 | 说明 |
|----|------|------|
| A | Virtual Account Entity Identifier | 实体标识，例如 `40006` |
| B | Virtual Account ID | **从最后位数开始修改**，对应 `vis` 账户表里的 id；例如数据库 id=123，就把末 3 位 `112` 改成 `123`。**千万不要改变位数，也不要改变格式** |
| C | Virtual Account Name | 用户姓名 |
| D | Virtual Account IBAN | 必须**唯一**，可使用日期段避免重复（示例 `AE270357414000620231020`） |
| E | Virtual Account Type | 例如 `Payment and Collection` |
| F | Hierarchy Type | 例如 `P` |

## 预期结果
- 激活成功 → 前端展示 IBAN 信息，DB 中 `status=Valid`
- 激活处理中 → DB 中 `status=Initial`，等待 `vis_ibanAccountRetryJob` 重试
- 无库存 → DB 落库无 IBAN，前端无 IBAN 展示，需按上述模板人工补 IBAN 后由 job 重试转为 Valid
- VIP 用户走 Free Active 流程，补充姓名后激活
- lean 用户绕过批次处理直接完成

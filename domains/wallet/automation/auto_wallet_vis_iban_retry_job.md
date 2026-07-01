---
id: auto_wallet_vis_iban_retry_job
object_type: AutomationAsset
name: vis_ibanAccountRetryJob 批次处理任务 (VAM IBAN 申请重试 Job)
aliases: [vis_ibanAccountRetryJob, IBAN Account Retry Job]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: legacy/wiki/vam-iban (automation_vis_iban_account_retry_job; confluence:tester/219152444)
tags: [wallet, vam, iban, vis, fab, batch, job, retry]
related_scenarios: [scn_wallet_vam_iban_apply_activate]
related_services: [svc_vis]
---

# vis_ibanAccountRetryJob 批次处理任务

## 用途
非 lean 场景下,fab 用户的 VAM IBAN 申请由该批次 Job 统一收口处理。fab 用户在 PayBy App 充值入口(Bank Account Transfer)点击激活后,申请记录通过 `mid` 关联落库到 [[tbl_vis_t_virtual_account]],初始 `status=Initial`;此后由 `vis_ibanAccountRetryJob` 批量打批发 fab,将 IBAN 数据状态更新为 `Valid`。覆盖除 lean 场景外所有 fab 用户的 IBAN 申请流程。

## 关联关系
- **覆盖的场景**:[[scn_wallet_vam_iban_apply_activate]](= `related_scenarios`)。
- **针对 / 跑在的服务**:[[svc_vis]](虚拟 IBAN 账户服务)(= `related_services`)。
- **校验的表**:[[tbl_vis_t_virtual_account]](申请记录主表,状态 Initial → Valid)。

## 使用方式
- Job 名称:`vis_ibanAccountRetryJob`。
- Job 触发后批量打批发 fab,更新 IBAN 数据状态为 `Valid`。
- 申请落库后的几种情形:
  - **正常**:`tbl_vis_t_virtual_account` 中 `status=Initial`,等待 Job 触发后调用 fab,更新为 `Valid`。
  - **无库存**:前端申请落库时无 IBAN 信息,需人工补录 IBAN 数据后,等待 Job 重试转 `Valid`。

## 关键配置
- 不调用 fab 的本地 mock 配置(仅用于测试,Job 不真实外呼):
  ```yaml
  vis:
    notification:
      mock: Y
  ```

## 注意事项
- **适用范围**:除 lean 场景外,其他 fab 用户的 IBAN 申请都走该批次 Job;lean 场景不走该 Job(直接处理)。
- VIP 用户点击 `Free Active` 按钮后需补充姓名信息,**无校验**。
- IBAN 库存为空时,落库无 IBAN 信息,需人工补录(导入模板规范见 [[scn_wallet_vam_iban_apply_activate]])后由 Job 重试。
- 申请落库表:[[tbl_vis_t_virtual_account]](通过 `mid` 关联),初始 `status=Initial`,Job 处理后更新为 `Valid`。
- 维护者 / 人工补录联系人:「待补 / 以实际为准」(原 wiki 历史信息)。

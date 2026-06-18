---
id: auto_vis_iban_account_retry_job
object_type: AutomationAsset
domain: vam-iban
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:tester/219152444
tags:
- job
- batch
- iban
- fab
subdomain: null
module: null
sensitivity: normal
name: vis_ibanAccountRetryJob 批次处理任务
aliases: []
related_services: []
related_tables:
- tbl_vis_t_virtual_account
related_scenarios:
- scn_vam_iban_apply_activate
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
处理非 lean 场景下 fab 用户的 IBAN 申请。fab 用户在 payby app 充值入口（Bank Account Transfer）点击激活后，申请记录落库到 vis.t_virtual_account（通过 mid 关联），初始 status=Initial，后续由该批次 job 统一处理。

## 使用方式
job 触发后，会打批发 fab，更新 iban 数据状态为 Valid。

申请落库后的几种情形：
- 正常情况：vis.t_virtual_account 中 status=Initial，等待 job 触发后调用 fab，状态更新为 Valid。
- 当 iban 没有库存时，前端申请落库是没有 iban 信息，可以人工补充 iban 数据后，等待 job 重试。

## 关键配置
mock 配置（不会调用 fab）：
```
vis:
  notification:
      mock: Y
```

## 注意事项
- 适用范围：除 lean 场景外，其他 fab 用户的 IBAN 申请都走该批次处理 job。
- Vip 用户点击 Free Active 按钮后，需要补充姓名信息，无校验。
- 当 iban 库存为空时，落库无 iban 信息，需要人工补录后由 job 重试。

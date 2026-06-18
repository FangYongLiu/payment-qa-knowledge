---
id: auto_vis_iban_account_retry_job
object_type: AutomationAsset
domain: payby-authorization-protocol
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:dc0d6822-f889-4a34-bdfe-72b5e0051862
tags:
- job
- iban
- fab
- retry
subdomain: vam-iban
module: vis
sensitivity: normal
name: IBAN账户重试Job
aliases:
- vis_ibanAccountRetryJob
related_services: []
related_tables:
- tbl_vis_t_virtual_account
related_scenarios:
- scn_vam_iban_apply_and_transaction
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
- 批次处理 fab 用户的 IBAN 申请
- job 触发后，打批发 fab，更新 IBAN 数据状态为 Valid
- 适用于除 lean 场景外，其他 fab 用户的 IBAN 申请流程

## 使用方式
- job 名称：vis_ibanAccountRetryJob
- 触发后批量调用 fab 完成 IBAN 数据状态更新
- 当 IBAN 没有库存时，前端申请落库没有 IBAN 信息，可人工添加 IBAN 数据后等待 job 重试

## 关键配置
- mock 配置（不会调用 fab）：
  ```
  vis:
    notification:
      mock: Y
  ```

## 注意事项
- 申请落库表为 vis.t_virtual_account（通过 mid 关联），初始 status=Initial，job 处理后更新为 Valid
- lean 场景不走该 job
- IBAN 库存为空时，前端申请落库不带 IBAN 信息，需人工补录后由 job 重试

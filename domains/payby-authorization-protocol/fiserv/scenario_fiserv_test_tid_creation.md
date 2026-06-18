---
id: scn_fiserv_test_tid_creation
object_type: Scenario
domain: payby-authorization-protocol
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:AQ/2199912473
tags:
- fiserv
- tid
- test-env
subdomain: fiserv
module: tms
sensitivity: normal
name: 测试环境构造Fiserv TID
aliases: []
related_services: []
related_tables:
- tbl_fiserv_out_bound
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
测试环境需要新的 Fiserv TID 用于设备绑定渠道（basis merchant → TMS → Activated Devices → Device Configuration），但生产 outbound 文件不会同步到测试环境，需要手动构造。

## 前置条件
- 有 `device.t_fiserv_out_bound` 表的写权限
- 待插入的 TID 在该表中不存在（不能重复）
- 已知 mid 前缀规则：
  - `1209` 开头：出租车公司
  - `7600` 开头：非出租车公司

## 操作步骤
1. 在 `device.t_fiserv_out_bound` 中手动插入一条记录
2. 设置 `config_status = 'INACTIVE'`
3. 文件路径字段不重要，可任意填写
4. 设置 TID（保证全表唯一）
5. 按 mid 前缀生成 `store_id`：
   - mid 以 `1209` 开头 → 将 mid 的前 2 位 `12` 替换为 `8116`，结果作为 store_id
   - mid 以 `7600` 开头 → 将 mid 的前 4 位 `7600` 替换为 `8116`，结果作为 store_id

## DB 校验点
- `device.t_fiserv_out_bound`
  - 新插入记录 `config_status='INACTIVE'`
  - TID 唯一
  - `store_id` 符合上述前缀替换规则

## 预期结果
- 在 basis merchant → TMS → Activated Devices → Fiserv Outbound Files 中能看到该 TID，状态为 Inactive
- 该 TID 可在 Device Configuration 中用于设备绑定渠道流程

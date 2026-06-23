---
id: scn_fiserv_test_env_mock_tid
object_type: Scenario
domain: payby-authorization-protocol
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:529d83bb-f8c0-47a4-af94-b05017e2e750
tags:
- fiserv
- test-env
- mock
- tid
subdomain: fiserv-channel
module: tms
sensitivity: normal
name: 测试环境创建并绑定Fiserv TID
aliases: []
related_services: []
related_tables:
- tbl_fiserv_out_bound
- tbl_fiserv_ping_url
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 触发/入口
测试环境需要新建并绑定一个Fiserv TID用于联调/测试。

## 前置条件
- 测试环境无法稳定接入Fiserv真实outbound文件流程，需手动构造数据。
- Fiserv测试环境虽可链接，但Fiserv不止给我们用，TID配置可能被改导致交易失败，因此一般用mock方式绑定渠道。

## 操作步骤
1. 在 `device.t_fiserv_out_bound` 中手动插入一条 `config_status='INACTIVE'` 的数据：
   - 文件路径不重要。
   - TID 不能重复。
   - mid 分两种：
     - `1209` 开头（出租车公司）：将 mid 的前 2 位换成 `8116`，作为 `store_id` 填入。
     - `7600` 开头（非出租车公司）：将 mid 的前 4 位换成 `8116`，作为 `store_id` 填入。
2. 渠道绑定使用 mock 方式（不走Fiserv真实测试环境），按 Fiserv 渠道绑定逻辑完成 server discovery → 注册 register_url → 获取并ping 4个 ping_url 的流程。
3. 在 basis merchant → TMS → Activated Devices → Activated Devices, Device Configuration 中输入该 Inactive 的 TID 完成设备绑定。

## DB 校验点
- `device.t_fiserv_out_bound`：手动插入的记录初始 `config_status='INACTIVE'`；绑定成功后该 TID 记录更新为 `ACTIVED`。
- `device.t_device_channel`：绑定成功后落一条 device_id 与 TID 关联的数据。
- `fiserv.t_ping_url`：4 个 ping_url 的 response time 已落库，且 `update_time` 在最近 6 小时内才视为有效。

## 预期结果
- 测试环境成功创建一条新的 Fiserv TID 并完成与设备的渠道绑定。
- 后续 POS 交易时，qpay-fsii 可从 `fiserv.t_ping_url` 中选取 `response_time_ms` 最小的有效 url 发送交易报文。

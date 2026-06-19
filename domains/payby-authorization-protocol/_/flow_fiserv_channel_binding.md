---
id: flow_fiserv_channel_binding
object_type: Flow
domain: authorization-protocol
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: wiki:529d83bb-f8c0-47a4-af94-b05017e2e750
tags:
- Fiserv
- TID
- 渠道绑定
- server-discovery
- ping-url
subdomain: null
module: qpay-fsii
sensitivity: normal
name: Fiserv渠道TID绑定流程
aliases: []
related_services: []
related_tables:
- tbl_fiserv_out_bound
- tbl_fiserv_ping_url
related_scenarios:
- scn_fiserv_test_env_mock_tid
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
Fiserv渠道TID绑定流程：从qpay-fsii发起server discovery服务发现，获取register_url后注册TID得到4个ping_url，再逐个ping以记录响应时间，完成端到端的渠道绑定。绑定成功后更新设备与TID关联记录。

## 步骤(跨系统)
1. **前置：Outbound文件落库**
   - Fiserv将outbound文件(.xml)上传至sftp
   - PayBy每天扫描sftp并解析为excel保存系统，数据落库 `device.t_fiserv_out_bound`，初始 `config_status='INACTIVE'`
   - 在 basis merchant → TMS → Activated Devices → Fiserv Outbound Files 中可查看解析到的所有TID

2. **设备扫码激活**

3. **设备绑定渠道TID**
   - 入口：basis merchant → TMS → Activated Devices → Activated Devices → Device Configuration
   - 输入在 Fiserv Outbound Files 中 `config_status=Inactive` 的TID

4. **Server Discovery（服务发现）**
   - qpay-fsii 使用配置文件中配置的 datawire url 请求 server discovery
   - 注册请求保存在 `fiserv.t_registration`
   - 返回 register_url，保存在 `fiserv.t_reg_url`，用于注册TID

5. **注册TID**
   - qpay-fsii 请求 register_url 注册TID
   - 返回 4 个 ping_url

6. **Ping 校验**
   - qpay-fsii 分别 ping 这 4 个 URL 确认连通
   - 将 ping 的 response time 保存到 `fiserv.t_ping_url`
   - Fiserv 要求每 6 小时重新获取一次 ping_url；系统只会把 `update_time` 在最近 6 小时之内的 url 视为有效 ping_url

7. **绑定结果落库**
   - `device.t_fiserv_out_bound` 中该TID记录更新为 `ACTIVED`
   - `device.t_device_channel` 落一条 device_id 与 TID 关联的数据

## 涉及服务/表
- 服务：qpay-fsii（持有 datawire url 配置，发起 server discovery、注册、ping）
- 表：
  - `device.t_fiserv_out_bound`（TID 来源与状态）
  - `fiserv.t_registration`（server discovery 注册请求）
  - `fiserv.t_reg_url`（register_url）
  - `fiserv.t_ping_url`（4个ping_url及response_time_ms）
  - `device.t_device_channel`（device_id 与 TID 关联）

## 校验点
- TID 来源必须为 `device.t_fiserv_out_bound` 中 `config_status='INACTIVE'` 的记录
- server discovery 成功后才能获得 register_url
- 注册成功后必须能 ping 通 4 个 ping_url，并写入 response_time
- 有效 ping_url 的判定：`update_time` 在最近 6 小时之内
- 绑定成功后状态变更：`device.t_fiserv_out_bound.config_status = ACTIVED`，且 `device.t_device_channel` 存在关联记录
- 测试环境一般使用 mock，因为 Fiserv 测试环境的TID配置可能被其他方修改导致交易失败

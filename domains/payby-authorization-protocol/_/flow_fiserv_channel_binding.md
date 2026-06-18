---
id: flow_fiserv_channel_binding
object_type: Flow
domain: payby-authorization-protocol
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:AQ/2199912473
tags:
- fiserv
- binding
- tms
subdomain: null
module: null
sensitivity: normal
name: Fiserv渠道绑定流程
aliases: []
related_services: []
related_tables:
- tbl_fiserv_out_bound
- tbl_fiserv_ping_url
related_scenarios:
- scn_fiserv_test_tid_creation
related_logs: []
related_requirements: []
related_failures: []
---

## 概述
Fiserv渠道绑定流程：从qpay-fsii请求datawire做server discovery开始，获取register_url后注册TID，得到4个ping_url并探测连通性，最终将TID激活并落库device_id与TID的关联关系。

## 步骤(跨系统)
1. **前置：Outbound文件落库**
   - Fiserv将outbound文件(原始为.xml格式)上传到sftp
   - PayBy每天扫描sftp文件，解析为excel格式保存到系统
   - 解析后的数据落库到 `device.t_fiserv_out_bound`，初始 `config_status='INACTIVE'`
   - 在 basis merchant → TMS → Activated Devices → Fiserv Outbound Files 目录中查看

2. **设备绑定TID入口**
   - basis merchant → TMS → Activated Devices → Activated Devices, Device Configuration
   - 输入在 Fiserv Outbound Files 中状态为 Inactive 的TID

3. **Server Discovery（服务发现）**
   - 配置用于 server discovery 的 datawire url 位于 qpay-fsii 配置文件中
   - 绑定时先请求 server discovery，注册请求保存在 `fiserv.t_registration`
   - 得到 register_url，保存在 `fiserv.t_reg_url`，用于注册TID

4. **注册TID**
   - qpay-fsii 请求 register_url 去注册TID
   - 得到 4 个 ping_url

5. **Ping探测**
   - qpay-fsii 分别 ping 这 4 个 URL 确保连通
   - 把 ping 的 response time 保存到 `fiserv.t_ping_url`
   - Fiserv 要求每 6 小时重新获取一次 ping_url，系统只会把 update_time 在最近 6 小时之内的 url 作为有效 ping_url

6. **激活落库**
   - 渠道绑定成功后，`device.t_fiserv_out_bound` 中该TID记录更新为 `ACTIVED`
   - `device.t_device_channel` 落一条 device_id 与 TID 关联的数据

## 涉及服务/表
- **服务**：qpay-fsii（持有 datawire url 配置；执行 server discovery、注册、ping）
- **表**：
  - `device.t_fiserv_out_bound`：outbound TID 数据，`config_status` 由 INACTIVE → ACTIVED
  - `fiserv.t_registration`：server discovery 注册请求
  - `fiserv.t_reg_url`：保存 register_url
  - `fiserv.t_ping_url`：保存 4 个 ping_url 及 response_time_ms，update_time 用于 6 小时有效期判断
  - `device.t_device_channel`：device_id 与 TID 关联

## 校验点
- 绑定输入的TID必须在 Fiserv Outbound Files 中且状态为 Inactive
- 测试环境构造TID时，TID 不能重复；mid 与 store_id 规则：1209开头(出租车)的mid把前2位替换为8116作为store_id；7600开头的mid把前4位替换为8116作为store_id
- 4个 ping_url 必须连通，response_time 落库
- 仅 update_time 在最近 6 小时之内的 ping_url 视为有效
- 绑定成功后须同时满足：t_fiserv_out_bound 状态为 ACTIVED 且 t_device_channel 写入关联记录
- 测试环境虽可连真实 Fiserv，但因其配置可能被改导致交易失败，一般使用 mock

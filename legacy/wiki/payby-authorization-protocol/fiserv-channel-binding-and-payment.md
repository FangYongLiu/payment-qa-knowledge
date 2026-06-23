---
title: Fiserv渠道绑定与支付流程
domain: authorization-protocol
kind: wiki_page
slug: fiserv-channel-binding-and-payment
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:529d83bb-f8c0-47a4-af94-b05017e2e750
tags: []
---

# Fiserv渠道绑定与支付流程

本页说明Fiserv渠道在PayBy系统中的接入方式，包括outbound文件解析、TID激活绑定、测试环境mock以及POS刷卡交易的全流程。

## Outbound文件解析

- Fiserv将outbound文件（原始为`.xml`格式）推送到sftp
- PayBy每天扫描sftp文件，解析为excel格式保存
- 解析后数据落库到 [[tbl_fiserv_out_bound]]，初始 `config_status='INACTIVE'`
- 在 basis merchant → TMS → Activated Devices → Fiserv Outbound Files 可查看所有解析到的TID数据

## 设备绑定渠道TID（生产）

操作路径：basis merchant → TMS → Activated Devices → Activated Devices → Device Configuration

输入在 Fiserv Outbound Files 中状态为 `INACTIVE` 的TID进行绑定。完整步骤参考 [[flow_fiserv_channel_binding]]。

绑定成功后：
- `device.t_fiserv_out_bound` 中该TID记录更新为 `ACTIVED`
- `device.t_device_channel` 落一条 device_id 与 TID 关联的数据

## 绑定逻辑（Server Discovery → Register → Ping）

1. 在 qpay-fsii 配置文件中维护用于 server discovery 的 datewire url
2. 请求 server discovery 做服务发现，注册请求保存在 `fiserv.t_registration`
3. 得到 `register_url`，保存在 `fiserv.t_reg_url`，用于注册TID
4. qpay-fsii 请求 `register_url` 注册，得到 4 个 ping_url
5. qpay-fsii 分别 ping 这 4 个 URL 确认连通性，并将 response time 保存至 [[tbl_fiserv_ping_url]]

> Fiserv 要求每 6 小时重新获取一次 ping_url，因此系统只把 `update_time` 在最近 6 小时之内的 url 视为有效。

## 测试环境mock新TID

测试环境可连接 Fiserv，但 Fiserv 测试环境为多方共用，给我们的TID有时会被改配置导致交易失败，因此一般使用 mock。详见 [[scn_fiserv_test_env_mock_tid]]。

向 `device.t_fiserv_out_bound` 手动插入 `config_status='INACTIVE'` 的数据：

- 文件路径不重要
- TID 不能重复
- `mid` 分两类：
  - `1209` 开头：出租车公司
  - `7600` 开头：非出租车公司
- `store_id` 规则：
  - `mid` 为 `1209` 开头：把 mid 前 2 位替换为 `8116` 作为 store_id
  - `mid` 为 `7600` 开头：把 mid 前 4 位替换为 `8116` 作为 store_id

## POS刷卡交易流程

- 在 POS 上点击下单：不调用任何接口
- POS 刷卡时：
  1. 先调下单接口，得到订单 `tokenUrl`
  2. 自动调支付接口
- qpay-fsii 收到交易请求后，从 [[tbl_fiserv_ping_url]] 中筛选 `response_time_ms` 最小（速度最快）的 url，向该 url 发送交易报文

完整时序参考 [[flow_fiserv_pos_payment]]。

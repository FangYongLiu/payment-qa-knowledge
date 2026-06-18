---
title: Fiserv渠道绑定与支付流程
domain: payby-authorization-protocol
kind: wiki_page
slug: fiserv-channel-binding-and-payment
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2199912473
tags: []
---

# Fiserv渠道绑定与支付流程

本页描述 Fiserv 渠道从 outbound 文件解析、TID 激活与绑定、测试环境 TID 构造，到 POS 刷卡交易请求路由的端到端流程。相关流程图见 [[flow_fiserv_channel_binding]] 与 [[flow_fiserv_pos_payment]]。

## Outbound 文件解析

- Fiserv 将 outbound 原始 `.xml` 文件投递到 SFTP。
- PayBy 每天扫描 SFTP 文件，解析后转为 excel 格式保存到系统内部。
- 解析后的数据落库到 [[tbl_fiserv_out_bound]]，初始 `config_status='INACTIVE'`。
- 解析结果可在 basis merchant → TMS → Activated Devices → **Fiserv Outbound Files** 中查看。

## 设备扫码激活与渠道绑定

- 入口：basis merchant → TMS → Activated Devices → **Activated Devices**, Device Configuration。
- 操作：输入在 **Fiserv Outbound Files** 中状态为 `Inactive` 的 TID 进行绑定。
- 绑定成功后：
  - `device.t_fiserv_out_bound` 中该 TID 记录更新为 `ACTIVED`。
  - `device.t_device_channel` 落一条 device_id 与 TID 的关联记录。

## 渠道绑定的内部逻辑

绑定动作由 `qpay-fsii` 驱动，流程如下：

1. **Server Discovery**：从 `qpay-fsii` 配置文件读取 datawire url，发起服务发现请求；该注册请求记录在 `fiserv.t_registration`。
2. 服务发现返回 `register_url`，保存到 `fiserv.t_reg_url`，用于 TID 注册。
3. `qpay-fsii` 请求 `register_url` 完成 TID 注册，返回 4 个 `ping_url`。
4. `qpay-fsii` 分别 ping 这 4 个 URL，确认连通，并将 response time 写入 [[tbl_fiserv_ping_url]]。
5. **有效期约束**：Fiserv 要求每 6 小时重新获取一次 ping_url，因此系统只把 `update_time` 在最近 6 小时内的 URL 视为有效 ping_url。

## 测试环境 TID 构造

详细操作见 [[scn_fiserv_test_tid_creation]]，规则要点：

- 在 `device.t_fiserv_out_bound` 手动插入 `config_status='INACTIVE'` 的记录。
- 文件路径不重要，**TID 不能重复**。
- `mid` 分两类：
  - `1209` 开头：出租车公司。`store_id` = 将 mid 的前 **2 位** 替换为 `8116`。
  - `7600` 开头：非出租车公司。`store_id` = 将 mid 的前 **4 位** 替换为 `8116`。

## 测试环境渠道绑定说明

- 测试环境可连接 Fiserv，但 Fiserv 测试环境为多方共用，其 TID 配置可能被改动导致交易失败。
- 因此一般使用 **mock** 进行测试。

## POS 刷卡交易路由

- 在 POS 上点击下单：不调用任何接口。
- POS 刷卡时：
  1. 先调下单接口得到订单 `tokenUrl`。
  2. 自动调支付接口。
- `qpay-fsii` 收到交易请求后，从 [[tbl_fiserv_ping_url]] 中选取 `response_time_ms` 最小（速度最快）的 URL，向其发送交易报文。

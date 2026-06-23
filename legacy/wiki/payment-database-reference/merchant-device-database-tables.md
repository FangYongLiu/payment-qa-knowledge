---
title: 商户与设备库常用表
domain: payment-database-reference
kind: wiki_page
slug: merchant-device-database-tables
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:79d1eee0-a479-47fd-8b3d-ec12172156f3
tags: []
---

# 商户与设备库常用表

本页汇总 `merchant`（商户库）、`device`（设备库）以及 `acs`（网关）相关常用表，便于快速定位商户/门店/员工、账期与定时出款、设备与激活码、以及网关接口权限与白名单等数据。

相关页面：[[common-database-tables-guide]] · [[member-database-tables]] · [[trade-statement-database-tables]] · [[pricing-database-tables]]

## merchant 商户库

| 表名 | 说明 |
| --- | --- |
| `merchant.t_merchant` | 商户表，`mid` 商户号，`id` 商户 id |
| `merchant.t_store` | 门店表，`merchant_id` 商户 id，`id` 门店 id |
| `merchant.t_staff` | 员工表，门店下员工 |
| `merchant.t_staff_role` | 员工角色表 |
| `merchant.t_period` | 账期表 |
| `merchant.t_auto_withdraw_registration` | 定时出款设置表 |
| `merchant.t_auto_withdraw_order` | 定时出款订单表 |

要点：
- 商户层级关系：商户（`t_merchant`）→ 门店（`t_store`，通过 `merchant_id` 关联）→ 员工（`t_staff`）。
- 员工权限通过 `t_staff_role` 维护。
- 账期与自动出款相关的登记/订单分别落在 `t_auto_withdraw_registration` 与 `t_auto_withdraw_order`。

## device 设备库

| 表名 | 说明 |
| --- | --- |
| `device.t_hardware_info` | 设备信息表 |
| `device.t_merchant_device` | 商户绑定设备表 |
| `device.t_active_code` | 激活码表 |
| `device.t_device_apply_order` | 设备申请列表 |
| `device.t_device_key` | 设备密钥表 |

要点：
- 设备实物信息查 `t_hardware_info`；商户与设备的绑定关系查 `t_merchant_device`。
- 设备激活、申请、密钥分别对应 `t_active_code`、`t_device_apply_order`、`t_device_key`。

## acs 网关相关

| 表名 | 说明 |
| --- | --- |
| `acs.t_key_config` | 公私钥配置 |
| `acs.t_gateway_merchant_api_auth` | 接口权限 |
| `acs.t_gateway_api_group` | 接口配置 |
| `acs.t_gateway_api_group_relation` | 接口分组关系 |
| `acs.t_reffer_list` | IP 白名单 |

要点：
- 排查商户调用接口是否被授权：先看 `t_gateway_merchant_api_auth`，再结合 `t_gateway_api_group` 与 `t_gateway_api_group_relation` 确认接口归属的分组。
- 验签问题查 `t_key_config`；来源 IP 拦截问题查 `t_reffer_list`。

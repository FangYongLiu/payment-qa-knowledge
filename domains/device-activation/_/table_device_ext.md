---
id: tbl_device_ext
object_type: Table
domain: device-activation
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:AQ/1135345829
tags:
- device
- ext
- config
subdomain: null
module: null
sensitivity: normal
name: 设备功能扩展配置表
aliases:
- t_device_ext
related_services: []
related_tables:
- tbl_merchant_device
related_scenarios:
- flow_device_activation
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
记录设备开通的功能配置，关联商户-设备关系。设备激活并建立商户-门店-设备关系后，在该表配置该设备开通的功能项。

## 关键列
- `device_id`：关联 `t_merchant_device.id`（商户-设备关系记录 id）

## 主键/索引
- 关联键：`device_id` → `t_merchant_device.id`
（原文未提供主键及其他索引信息）

## 校验点(QA 关注)
- 设备激活完成后，校验 `t_device_ext` 中是否按 `device_id=t_merchant_device.id` 落库对应功能配置
- `device_id` 必须能在 `t_merchant_device` 中查到对应记录（即设备已完成激活并建立商户-门店-设备关系）
- 查询语句：`select * from device.t_device_ext;`

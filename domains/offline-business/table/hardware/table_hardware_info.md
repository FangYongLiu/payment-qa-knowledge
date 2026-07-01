---
id: tbl_hardware_info
object_type: Table
name: 设备硬件信息表(device.t_hardware_info)
aliases:
- t_hardware_info
- device.t_hardware_info
domain: offline-business
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/1135345829
tags:
- 设备激活
- 硬件信息
- SmartPOS
related_services: [svc_device]
related_scenarios: []
---

# 设备硬件信息表(device.t_hardware_info)

## 用途
`device.t_hardware_info` 保存设备首次激活后的物理硬件信息。设备扫描激活二维码完成激活后，系统向该表写入一条记录，登记该设备的物理序列号(`SN`)与激活的设备类型(`type`)，作为该硬件设备在收单体系中的唯一身份锚点。后续 POS 交易通过商户-设备关系定位到该硬件。详见 [[flow_device_activation]]。

库表:`device.t_hardware_info`

## 关联关系
- **所属服务**:[[svc_device]](= frontmatter `related_services`)
- **上游联动**:[[tbl_active_code]](激活码 `USED` 时本表新增记录)、[[tbl_device_apply_order]](申请单决定 `type` 取值)。
- **下游引用**:[[tbl_merchant_device]](`t_merchant_device.hardware_id = t_hardware_info.id`，绑定商户与硬件);`device.t_device_key`(`t_device_key.id = t_hardware_info.id`，登记设备公钥，待补对象)。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | 待补 | 主键，被 `t_device_key.id`、`t_merchant_device.hardware_id` 外键引用 |
| `SN` | 待补 | 物理设备序列号，应与实际硬件一致 |
| `type` | 待补 | 激活的设备类型(本场景为 `Smart POS`)，应与申请单设备类型一致 |

## 主键 / 索引
- 主键:`id`(被 `t_device_key.id`、`t_merchant_device.hardware_id` 外键引用)。
- 业务唯一性:物理 `SN` 在正常流程下应保持唯一，不应重复激活。

## 校验点(QA 关注)
- **新增记录**:设备首次激活成功后应新增一条记录，`SN` 与物理设备序列号一致、`type` 与申请单设备类型(Smart POS)一致。
- **外键一致性**:同一次激活动作，`t_hardware_info.id` 应能在 `t_device_key.id` 与 [[tbl_merchant_device]] 的 `hardware_id` 中关联到对应记录，三者一一对应。
- **激活码联动**:与 [[tbl_active_code]] 联动校验——激活码状态由 `ENABLE` 变为 `USED` 的同时，本表应同步生成对应硬件记录，时间戳在合理窗口内。
- **与申请单一致**:`type` 应回溯匹配 [[tbl_device_apply_order]] 中该笔申请的设备类型，避免类型错配。
- **唯一性**:同一物理 `SN` 在正常激活流程下不应出现重复记录(如有重复需排查重复激活/脏数据)。

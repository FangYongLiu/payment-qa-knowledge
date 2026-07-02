---
id: tbl_aml_t_device_base_info
object_type: Table
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (aml schema) 2026-06-25
tags:
- aml
- aml
- t_device_base_info
subdomain: aml
module: null
sensitivity: normal
name: 设备基本信息表(t_device_base_info)
aliases:
- t_device_base_info
related_services:
- svc_aml
related_scenarios: []
---
# 设备基本信息表(t_device_base_info)

## 用途
设备基本信息表。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键 |
| `session_id` | varchar(64) | NOT NULL | session id |
| `agent_brand` | varchar(32) |  | 终端品牌 |
| `agent_language` | varchar(32) |  | 终端语言 |
| `agent_locale` | varchar(20) |  | 终端语言环境 |
| `agent_model` | varchar(32) |  | 终端型号 |
| `agent_type` | varchar(32) |  | 终端类型 |
| `agent_app_info` | varchar(64) |  | 终端接入应用信息 |
| `device_id` | varchar(32) |  | 设备id |
| `device_id_confidence` | varchar(20) |  | 设备ID置信度 |
| `fuzzy_device_id` | varchar(32) |  | 模糊设备ID |
| `fuzzy_device_id_confidence` | varchar(20) |  | 模糊设备ID置信度 |
| `screen_res` | varchar(20) |  | 屏幕分辨率 |
| `os` | varchar(64) |  | 系统 |
| `os_fonts_hash` | varchar(32) |  | 系统字体hash值 |
| `os_fonts_number` | varchar(10) |  | 系统字体数量 |
| `ua_os` | varchar(64) |  | 系统类型 |
| `os_version` | varchar(64) |  | 系统版本 |
| `agent_profiling_delta` | varchar(20) |  | 终端咨询耗时(毫秒) |
| `agent_bssid` | varchar(20) |  | 终端BSSID |
| `agent_connection_type` | varchar(32) |  | 终端连接方式 |
| `ua_os_alt` | varchar(64) |  | 系统 |
| `ua_os_version_alt` | varchar(20) |  | 系统版本 |
| `device_model` | varchar(32) |  | 设备型号 |
| `device_name` | varchar(32) |  | 设备名称 |
| `device_imei` | varchar(64) |  | 设备IMEI |
| `create_time` | timestamp | 默认 CURRENT_TIMESTAMP | 创建时间 |
| `update_time` | timestamp | 默认 CURRENT_TIMESTAMP | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `create_time_session_id` (create_time, session_id)
  - `session_id` (session_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

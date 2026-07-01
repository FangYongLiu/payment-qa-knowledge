---
id: tbl_aml_t_device_expand_info
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
- t_device_expand_info
subdomain: aml
module: null
sensitivity: normal
name: 设备扩展信息表(t_device_expand_info)
aliases:
- t_device_expand_info
related_services:
- svc_aml
related_scenarios: []
---
# 设备扩展信息表(t_device_expand_info)

## 用途
设备扩展信息表。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键 |
| `session_id` | varchar(64) | NOT NULL | session id |
| `browser_language` | varchar(20) |  | 浏览器语言 |
| `browser_string` | varchar(512) |  | 浏览器信息 |
| `http_os_signature` | varchar(128) |  | http签名 |
| `jb_root` | varchar(8) |  | 越狱可能性 |
| `jb_root_reason` | varchar(256) |  | 越狱理由 |
| `js_browser_string` | varchar(512) |  | 浏览器信息 |
| `page_time_on` | varchar(10) |  | 页面停留时间 |
| `plugin_number` | varchar(10) |  | 插件数量(仅适用于非IE浏览器) |
| `policy_score` | varchar(5) |  | 策略分值 |
| `profiling_datetime` | varchar(10) | 默认 '0' | 咨询时间戳 |
| `ua_browser` | varchar(32) |  | 浏览器类型 |
| `ua_mobile` | varchar(16) |  | 是否移动设备 |
| `virtual_device` | varchar(5) |  | 是否模拟器设备(大于0的数值都有可能) |
| `virtual_device_reason` | varchar(256) |  | 是模拟器设备理由 |
| `device_health_reasons` | varchar(256) |  | 设备健康理由 |
| `digital_id` | varchar(64) |  | 身份ID |
| `digital_id_confidence` | varchar(10) |  | 身份ID置信度(越高置信度越高) |
| `ua_browser_alt` | varchar(32) |  | 浏览器类型 |
| `ua_browser_version_alt` | varchar(20) |  | 浏览器版本 |
| `web_session_id` | varchar(64) |  | WEB会话ID |
| `digital_id_confidence_rating` | varchar(64) |  | LexID数字置信度等级 |
| `agent_boot_time` | varchar(32) |  | 终端启动时间 |
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

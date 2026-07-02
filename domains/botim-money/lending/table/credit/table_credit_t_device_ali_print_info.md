---
id: tbl_credit_t_device_ali_print_info
object_type: Table
name: Device Ali fingerprint identification information table (t_device_ali_print_info)
aliases: [t_device_ali_print_info, credit.t_device_ali_print_info]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: credit schema DDL
tags: [lending, credit]
sensitivity: normal
related_services: []
---

# Device Ali fingerprint identification information table (t_device_ali_print_info)

## 用途
物理表 `credit.t_device_ali_print_info`,主键 `id`。Device Ali fingerprint identification information table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key ID · 可空 |
| `device_id` | varchar(64) | Device ID · 可空 |
| `apdid` | varchar(64) | apdid (unique) · 可空 |
| `conn` | int | Connection type: 1=wifi, 2=4g, 3=5g, etc. · 可空 |
| `cpu_model` | varchar(32) | CPU model · 可空 |
| `language` | varchar(32) | Language setting: e.g., en, en_US · 可空 |
| `install_time` | bigint | App installation time (Unix timestamp) · 可空 |
| `battery` | int | Battery level: -1 means unknown · 可空 |
| `charge_status` | int | Charging status: 0=not charging, 1=charging, 3=charging · 可空 |
| `resolution` | varchar(32) | Screen resolution: e.g., 1080,2280 · 可空 |
| `avail_sto` | bigint | Available storage space (bytes) · 可空 |
| `os_ver` | varchar(16) | Operating system version: e.g., 9, 16.2 · 可空 |
| `phone_model` | varchar(64) | Phone model: e.g., SM-G975F, iPhone · 可空 |
| `wifi_dns` | varchar(64) | WiFi DNS address · 可空 |
| `mem` | bigint | Total memory (bytes) · 可空 |
| `inter_ip` | varchar(64) | Internal IP address · 可空 |
| `avail_mem` | bigint | Available memory (bytes) · 可空 |
| `client_ip` | varchar(64) | Client IP address · 可空 |
| `brand` | varchar(32) | Device brand: e.g., Apple, Samsung, etc. · 可空 |
| `cpu_core` | int | CPU cores · 可空 |
| `os` | varchar(16) | Operating system: iOS, Android, etc. · 可空 |
| `boot_time` | bigint | System boot time (Unix timestamp) · 可空 |
| `app_ver` | varchar(32) | App version: e.g., 4.4.1 · 可空 |
| `wifi_status` | int | WiFi status: 0=off, 1=on, 2=connecting, 3=connected · 可空 |
| `custom_name` | varchar(64) | Custom device name: e.g., Galaxy S10+ · 可空 |
| `cpu_name` | varchar(64) | CPU name · 可空 |
| `sto` | bigint | Total storage space (bytes) · 可空 |
| `wifi_gateway` | varchar(64) | WiFi gateway address · 可空 |
| `local_time` | bigint | Local time (Unix timestamp) · 可空 |
| `brightness` | int | Screen brightness: 0-255 · 可空 |
| `risk_labels` | varchar(128) | Risk labels list (JSON string): e.g., ["threat_behavior_repack"] · 可空 |
| `wifi_mask` | varchar(64) | WiFi subnet mask · 可空 |
| `cpu_max_freq` | bigint | CPU max frequency · 可空 |
| `phone_name` | varchar(64) | Device name: e.g., beyond2ltexx · 可空 |
| `width` | int | Screen width · 可空 |
| `height` | int | Screen height · 可空 |
| `sdk_ver` | varchar(64) | SDK version · 可空 |
| `android_id` | varchar(64) | Android ID · 可空 |
| `mac` | varchar(32) | MAC address · 可空 |
| `wlan_mac` | varchar(32) | WLAN MAC address · 可空 |
| `switches` | varchar(255) | Switches status (JSON string): mobileData, wifi, bluetooth, gps, etc. · 可空 |
| `permissions` | varchar(2048) | App permissions (JSON string) · 可空 |
| `risk_labels_times` | varchar(128) | Risk labels times (JSON string) · 可空 |
| `created_time` | datetime | Created time · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_apdid`:apdid (UNIQUE)
- `idx_created_time`:created_time
- `idx_device_id`:device_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

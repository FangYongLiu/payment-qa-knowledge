---
id: tbl_devicefpii_real_time_device_risk_statistics
object_type: Table
name: real_time_device_risk_statistics (real_time_device_risk_statistics)
aliases: [real_time_device_risk_statistics, devicefpii.real_time_device_risk_statistics]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: devicefpii schema DDL
tags: [risk, devicefpii]
sensitivity: normal
related_services: []
---

# real_time_device_risk_statistics (real_time_device_risk_statistics)

## 用途
物理表 `devicefpii.real_time_device_risk_statistics`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 · 可空 |
| `app_id` | varchar(40) | Id |
| `record_time` | varchar(255) | :"2017-09-11 09:11" |
| `ios_hook` | int(8) | [ios]HOOK |
| `ios_jailbreak` | int(8) | [ios] |
| `ios_inject` | int(8) | [ios] |
| `ios_debug` | int(8) | [ios]debug |
| `ios_is_frame_attack` | int(8) | [ios] |
| `ios_emulator` | int(8) | [ios] |
| `ios_is_vpn` | int(8) | [ios]VPN |
| `ios_is_proxy` | int(8) | [ios] |
| `ios_multirun` | int(8) | [ios] |
| `android_emulator` | int(8) | [android] |
| `android_inject` | int(8) | [android] |
| `android_dump` | int(8) | [android]dump |
| `android_debug` | int(8) | [android]debug |
| `android_multirun` | int(8) | [android] |
| `android_flaw_janus` | int(8) | [android] |
| `android_device_root` | int(8) | [android]root |
| `android_is_vpn` | int(8) | [android]VPN |
| `android_is_proxy` | int(8) | [android] |
| `android_is_frame_attack` | int(8) | [android] |
| `android_other` | int(8) | [android] |
| `ios_other` | int(8) | [ios] |
| `req_num` | int(8) | 待补 |
| `risk_num` | int(8) | 待补 |
| `crash_num` | int(8) | 待补 · 可空 |
| `create_time` | timestamp | 待补 |
| `modify_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `un_record_time_app_id`:record_time, app_id (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_devicefpii_user_active_statistics
object_type: Table
name: user_active_statistics (user_active_statistics)
aliases: [user_active_statistics, devicefpii.user_active_statistics]
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

# user_active_statistics (user_active_statistics)

## 用途
物理表 `devicefpii.user_active_statistics`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 · 可空 |
| `app_id` | varchar(40) | id |
| `record_time` | varchar(255) | :"2017-09-11 09:11" |
| `device_type` | int(4) | 1android 2ios 3windows 4mac |
| `new_user_num` | int(8) | 新增设备 |
| `risk_user_num` | int(8) | 活跃用户中 风险设备数 |
| `active_user_num` | int(8) | 新增活跃 |
| `create_time` | timestamp | 待补 |
| `modify_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `un_record_time_app_id_device_type`:record_time, app_id, device_type (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

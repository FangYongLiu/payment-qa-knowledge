---
id: tbl_devicefp_device_score_scale
object_type: Table
name: device_score_scale (device_score_scale)
aliases: [device_score_scale, devicefp.device_score_scale]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: devicefp schema DDL
tags: [risk, devicefp]
sensitivity: normal
related_services: []
---

# device_score_scale (device_score_scale)

## 用途
物理表 `devicefp.device_score_scale`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 · 可空 |
| `app_id` | varchar(40) | id |
| `device_type` | int(4) | 1web 2ios 3android |
| `score_slot` | int(4) | 0-9 |
| `num` | int(8) | 待补 |
| `create_time` | timestamp | 待补 |
| `modify_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `un_create_time_app_id_device_type_score_slot`:create_time, app_id, device_type, score_slot (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

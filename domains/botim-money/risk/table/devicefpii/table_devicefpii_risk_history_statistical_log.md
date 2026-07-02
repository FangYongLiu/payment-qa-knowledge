---
id: tbl_devicefpii_risk_history_statistical_log
object_type: Table
name: risk_history_statistical_log (risk_history_statistical_log)
aliases: [risk_history_statistical_log, devicefpii.risk_history_statistical_log]
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

# risk_history_statistical_log (risk_history_statistical_log)

## 用途
物理表 `devicefpii.risk_history_statistical_log`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `type` | int | ,1:,2: |
| `record_time` | varchar(255) | :"2017-09-11 09:11" |
| `create_time` | timestamp | 待补 |
| `modify_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `un_record_time_and_type`:record_time, type (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

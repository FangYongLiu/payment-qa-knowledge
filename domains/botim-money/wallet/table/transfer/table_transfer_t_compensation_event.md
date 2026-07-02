---
id: tbl_transfer_t_compensation_event
object_type: Table
name: 补偿事件 (t_compensation_event)
aliases: [t_compensation_event, transfer.t_compensation_event]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: transfer schema DDL
tags: [wallet, transfer]
sensitivity: normal
related_services: []
---

# 补偿事件 (t_compensation_event)

## 用途
物理表 `transfer.t_compensation_event`,主键 `event_id`。补偿事件。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `event_id` | bigint | 事件id · 可空 |
| `event_key` | varchar(64) | 事件主体标志 |
| `main_type` | varchar(32) | 事件主类型 |
| `sub_type` | varchar(32) | 事件子类型 |
| `execute_status` | char | 执行状态：I=初始，F=失败，S=成功，E=异常 |
| `execute_count` | int | 执行次数 |
| `extension` | varchar(255) | 扩展信息 · 可空 |
| `error_message` | varchar(128) | 错误信息 · 可空 |
| `allow_time` | timestamp | 允许执行时间 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`event_id`
- `uk_event_key_type_subtype`:event_key, main_type, sub_type (UNIQUE)
- `idx_allow_time`:allow_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

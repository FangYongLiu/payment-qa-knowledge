---
id: tbl_upic_t_hce_operation_record
object_type: Table
name: HCE操作记录 (t_hce_operation_record)
aliases: [t_hce_operation_record, upic.t_hce_operation_record]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: upic schema DDL
tags: [card, upic]
sensitivity: normal
related_services: []
---

# HCE操作记录 (t_hce_operation_record)

## 用途
物理表 `upic.t_hce_operation_record`,主键 `record_id`。HCE操作记录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `record_id` | bigint | 记录id：前八后九 |
| `member_id` | varchar(20) | 会员id |
| `device_id` | varchar(64) | 设备id |
| `host_app` | varchar(32) | hostApp |
| `operation_type` | varchar(32) | 操作类型：CLOSE=关闭 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `create_time` | timestamp | 创建时间 |

## 主键 / 索引
- 主键:`record_id`
- `idx_create_time_member_id`:create_time, member_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

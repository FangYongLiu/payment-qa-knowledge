---
id: tbl_member_t_compensation_event
object_type: Table
domain: activation
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (member schema) 2026-06-25
tags:
- member
- infra
- t_compensation_event
subdomain: infra
module: null
sensitivity: normal
name: 补偿事件(t_compensation_event)
aliases:
- t_compensation_event
related_services:
- svc_member
related_scenarios: []
---

# 补偿事件(t_compensation_event)

## 用途
补偿事件。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `event_id` | bigint | PK | 事件id |
| `event_key` | varchar(64) | NOT NULL | 事件主体标志 |
| `main_type` | varchar(32) | NOT NULL | 事件主类型 |
| `sub_type` | varchar(32) | NOT NULL | 事件子类型 |
| `execute_status` | char | NOT NULL | 执行状态：I=初始，F=失败，S=成功，E=异常 |
| `execute_count` | int | NOT NULL | 执行次数 |
| `extension` | varchar(255) |  | 扩展信息 |
| `error_message` | varchar(128) |  | 错误信息 |
| `allow_time` | timestamp |  | 允许执行时间 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`event_id`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

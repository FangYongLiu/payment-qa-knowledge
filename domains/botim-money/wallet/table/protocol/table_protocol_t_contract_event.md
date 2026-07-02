---
id: tbl_protocol_t_contract_event
object_type: Table
name: 协议事件表 (t_contract_event)
aliases: [t_contract_event, protocol.t_contract_event]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: protocol schema DDL
tags: [wallet, protocol]
sensitivity: normal
related_services: []
---

# 协议事件表 (t_contract_event)

## 用途
物理表 `protocol.t_contract_event`,主键 `id`。协议事件表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键ID |
| `sign_info_id` | bigint(25) | 签订的协议ID |
| `event_type` | varchar(35) | 事件类型 |
| `status` | varchar(15) | 事件状态 |
| `finish_time` | datetime | 完成时间 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- `idx_createtime`:create_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

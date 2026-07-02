---
id: tbl_rnpl_t_contract_deal_event
object_type: Table
name: Contract Processing Log Table (t_contract_deal_event)
aliases: [t_contract_deal_event, rnpl.t_contract_deal_event]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: rnpl schema DDL
tags: [lending, rnpl]
sensitivity: normal
related_services: []
---

# Contract Processing Log Table (t_contract_deal_event)

## 用途
物理表 `rnpl.t_contract_deal_event`,主键 `id`。Contract Processing Log Table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `contract_id` | int | contract id |
| `type` | tinyint | Event Type: 1:Contract Submission;2:Audit Completed;3:Down Payment Successful |
| `create_time` | timestamp | create time |
| `memo` | varchar(64) | memo · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_id`:contract_id, type (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

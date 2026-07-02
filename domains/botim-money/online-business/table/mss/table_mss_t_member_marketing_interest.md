---
id: tbl_mss_t_member_marketing_interest
object_type: Table
name: Member活动权益表 (t_member_marketing_interest)
aliases: [t_member_marketing_interest, mss.t_member_marketing_interest]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mss schema DDL
tags: [online-business, mss]
sensitivity: normal
related_services: []
---

# Member活动权益表 (t_member_marketing_interest)

## 用途
物理表 `mss.t_member_marketing_interest`,主键 `id`。Member活动权益表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 |
| `create_time` | timestamp | 创建时间 |
| `remarks` | varchar(128) | 备注 · 可空 |
| `update_time` | timestamp | 更新时间 |
| `member_id` | varchar(64) | MemberId |
| `status` | varchar(20) | 权益状态 |
| `interest_id` | bigint | 权益Id |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

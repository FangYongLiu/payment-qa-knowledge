---
id: tbl_upic_t_member_card_relation
object_type: Table
name: 会员卡关系 (t_member_card_relation)
aliases: [t_member_card_relation, upic.t_member_card_relation]
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

# 会员卡关系 (t_member_card_relation)

## 用途
物理表 `upic.t_member_card_relation`,主键 `relation_id`。会员卡关系。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `relation_id` | bigint | 关系id：前八后九 |
| `member_id` | varchar(20) | 会员id |
| `card_id` | bigint | 卡id |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`relation_id`
- `uk_member_id`:member_id (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

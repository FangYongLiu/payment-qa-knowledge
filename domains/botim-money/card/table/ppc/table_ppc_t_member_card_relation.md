---
id: tbl_ppc_t_member_card_relation
object_type: Table
name: Member card relation (t_member_card_relation)
aliases: [t_member_card_relation, ppc.t_member_card_relation]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ppc schema DDL
tags: [card, ppc]
sensitivity: normal
related_services: []
---

# Member card relation (t_member_card_relation)

## 用途
物理表 `ppc.t_member_card_relation`,主键 `relation_id`。Member card relation。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `relation_id` | bigint | ID |
| `member_id` | varchar(20) | Member ID |
| `eid_hash` | varchar(68) | Id hash, separate by prefix, PP=Passport, default is EID |
| `card_type` | char(2) | Card Type: MC=Multi-Currency, PR=Payroll |
| `related_times` | tinyint | Related Times · 可空 |
| `virtual_card_id` | bigint | Virtual Card ID · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`relation_id`
- `uk_member_id_card_type`:member_id, card_type (UNIQUE)
- `idx_eid_hash`:eid_hash
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

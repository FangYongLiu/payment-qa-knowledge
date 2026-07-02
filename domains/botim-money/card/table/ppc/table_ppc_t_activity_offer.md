---
id: tbl_ppc_t_activity_offer
object_type: Table
name: Activity Offer (t_activity_offer)
aliases: [t_activity_offer, ppc.t_activity_offer]
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

# Activity Offer (t_activity_offer)

## 用途
物理表 `ppc.t_activity_offer`,主键 `offer_id`。Activity Offer。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `offer_id` | bigint | Offer Id · 可空 |
| `offer_type` | varchar(10) | Offer Type: APC_ZP=Apply Physical Card Zero Pay |
| `member_id` | varchar(20) | Member Id |
| `source` | varchar(32) | Source: CASHNOW |
| `status` | char | Status: I=Init, U=Used |
| `sponsor_member_id` | varchar(20) | Sponsor Member ID · 可空 |
| `expire_time` | timestamp | Expire Time · 可空 |
| `finish_time` | timestamp | Finish Time · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `create_time` | timestamp | Create Time |
| `update_time` | timestamp | Update Time |

## 主键 / 索引
- 主键:`offer_id`
- `idx_finish_time`:finish_time
- `idx_member_id_offer_type`:member_id, offer_type
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

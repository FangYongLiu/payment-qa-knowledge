---
id: tbl_ppc_t_card_notify
object_type: Table
name: Card Notify (t_card_notify)
aliases: [t_card_notify, ppc.t_card_notify]
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

# Card Notify (t_card_notify)

## 用途
物理表 `ppc.t_card_notify`,主键 `notify_id`。Card Notify。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `notify_id` | bigint | Notify ID: 8 digits date time + 9 digits sequence |
| `member_id` | varchar(20) | Member ID |
| `card_type` | char(2) | Card Type |
| `notify_type` | varchar(20) | Notify Type |
| `virtual_card_id` | bigint | Virtual Card ID |
| `extension` | varchar(255) | Extension · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`notify_id`
- `uk_member_id_card_type_notify_type_vcId`:member_id, card_type, notify_type, virtual_card_id (UNIQUE)
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

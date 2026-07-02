---
id: tbl_ppc_t_virtual_card_extend
object_type: Table
name: Virtual Card Extend (t_virtual_card_extend)
aliases: [t_virtual_card_extend, ppc.t_virtual_card_extend]
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

# Virtual Card Extend (t_virtual_card_extend)

## 用途
物理表 `ppc.t_virtual_card_extend`,主键 `virtual_card_id`。Virtual Card Extend。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `virtual_card_id` | bigint | Virtual Card ID, 前八后九 |
| `physical_card_apply_id` | bigint | Physical Card Apply ID · 可空 |
| `close_card_fee_request_no` | bigint | Close Card Fee Request No: 凭证号 · 可空 |
| `close_card_source` | char(3) | Close Card Source: AC=App Close, AR=App Replace, PC=Portal Close, ACD=App Close Directly, ARP=App replace with pay · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `memo` | varchar(100) | Memo · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`virtual_card_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

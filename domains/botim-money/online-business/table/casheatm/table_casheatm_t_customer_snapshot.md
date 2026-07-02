---
id: tbl_casheatm_t_customer_snapshot
object_type: Table
name: 客户快照 (t_customer_snapshot)
aliases: [t_customer_snapshot, casheatm.t_customer_snapshot]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: casheatm schema DDL
tags: [online-business, casheatm]
sensitivity: normal
related_services: []
---

# 客户快照 (t_customer_snapshot)

## 用途
物理表 `casheatm.t_customer_snapshot`,主键 `global_id`。客户快照。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint | 全局号 |
| `nick_name` | varchar(200) | 待补 · 可空 |
| `masked_mobile_number` | varchar(200) | 待补 · 可空 |
| `partner_id` | varchar(200) | partner_id · 可空 |

## 主键 / 索引
- 主键:`global_id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

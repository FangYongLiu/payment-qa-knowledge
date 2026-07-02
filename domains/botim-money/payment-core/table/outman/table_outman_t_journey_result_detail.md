---
id: tbl_outman_t_journey_result_detail
object_type: Table
name: Member ID (t_journey_result_detail)
aliases: [t_journey_result_detail, outman.t_journey_result_detail]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: outman schema DDL
tags: [payment-core, outman]
sensitivity: normal
related_services: []
---

# Member ID (t_journey_result_detail)

## 用途
物理表 `outman.t_journey_result_detail`,主键 `id`。Member ID。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key |
| `journey_order_id` | bigint | Journey order id |
| `member_id` | varchar | 待补 · 可空 |

## 主键 / 索引
- 主键:`id`
- `j_order_id_idx`:journey_order_id
- `mid_idx`:member_id
- `req_no_idx`:request_no

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_ppc_t_work_order
object_type: Table
name: Work Order (t_work_order)
aliases: [t_work_order, ppc.t_work_order]
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

# Work Order (t_work_order)

## 用途
物理表 `ppc.t_work_order`,主键 `work_order_id`。Work Order。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `work_order_id` | bigint | Work Order ID |
| `work_order_type` | varchar(16) | Work Order Type: DELIVERY |
| `work_order_source` | char(2) | Work Order Source: SA=Statement Apply |
| `source_id` | bigint | Source ID |
| `status` | varchar(2) | Status |
| `extension` | varchar(255) | Extension · 可空 |
| `memo` | varchar(100) | Memo · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`work_order_id`
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

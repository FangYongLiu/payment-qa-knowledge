---
id: tbl_reconciliation_t_escrow_adjust_detail
object_type: Table
name: Escrow Adjust Detail Table (t_escrow_adjust_detail)
aliases: [t_escrow_adjust_detail, reconciliation.t_escrow_adjust_detail]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: reconciliation schema DDL
tags: [settlement, reconciliation]
sensitivity: normal
related_services: []
---

# Escrow Adjust Detail Table (t_escrow_adjust_detail)

## 用途
物理表 `reconciliation.t_escrow_adjust_detail`,主键 `detail_id`。Escrow Adjust Detail Table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `detail_id` | bigint | Detail Id: 8 digits date + 9 digits sequence |
| `adjust_id` | bigint | Adjust Id |
| `settlement_detail_id` | bigint | Settlement Detail Id |
| `extension` | varchar(255) | Extension · 可空 |
| `memo` | varchar(255) | Memo · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`detail_id`
- `idx_adjustId`:adjust_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

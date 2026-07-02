---
id: tbl_reconciliation_t_accounting_relate_order
object_type: Table
name: 自动登账详情表 (t_accounting_relate_order)
aliases: [t_accounting_relate_order, reconciliation.t_accounting_relate_order]
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

# 自动登账详情表 (t_accounting_relate_order)

## 用途
物理表 `reconciliation.t_accounting_relate_order`,主键 `id`。自动登账详情表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `source_type` | varchar(32) |  |
| `operation_type` | char(3) | 操作类型: A:登账  FO:提现 |
| `accounting_voucher_no` | varchar(32) | 订单号 · 可空 |
| `source_identity` | varchar(32) | 来源标志: 计提单id或计提批次单id |
| `status` | char | 状态:P:处理中 F:失败 S:成功 · 可空 |
| `memo` | varchar(100) | 备注 · 可空 |
| `extension` | varchar(255) | 扩展信息 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- `uk_accounting_voucher_no`:accounting_voucher_no (UNIQUE)
- `idx_source_identity`:source_identity
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

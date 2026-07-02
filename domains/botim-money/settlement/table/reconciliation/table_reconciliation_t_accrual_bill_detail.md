---
id: tbl_reconciliation_t_accrual_bill_detail
object_type: Table
name: 成本收入计提业务明细表 (t_accrual_bill_detail)
aliases: [t_accrual_bill_detail, reconciliation.t_accrual_bill_detail]
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

# 成本收入计提业务明细表 (t_accrual_bill_detail)

## 用途
物理表 `reconciliation.t_accrual_bill_detail`,主键 `detail_id`。成本收入计提业务明细表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `detail_id` | bigint | 明细id |
| `bill_id` | bigint | 计提单id |
| `source_type` | char(3) | 计提来源类型: FI:资金对账收入 CA:成本账号 TRV:手续费收入表 TRF:手续费退款表 |
| `detail_identity` | varchar(64) | Detail Identity |
| `source_account` | varchar(32) | 来源账户 · 可空 |
| `accrual_amount` | decimal(19, 4) | 计提金额 |
| `currency` | char(3) | 币种 |
| `extension` | varchar(255) | 扩展信息 · 可空 |
| `memo` | varchar(100) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |

## 主键 / 索引
- 主键:`detail_id`
- `uk_detail_type`:detail_identity, source_type (UNIQUE)
- `idx_bill_id`:bill_id
- `idx_create_time`:create_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

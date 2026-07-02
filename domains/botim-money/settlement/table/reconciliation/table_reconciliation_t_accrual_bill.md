---
id: tbl_reconciliation_t_accrual_bill
object_type: Table
name: 成本收入计提单表 (t_accrual_bill)
aliases: [t_accrual_bill, reconciliation.t_accrual_bill]
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

# 成本收入计提单表 (t_accrual_bill)

## 用途
物理表 `reconciliation.t_accrual_bill`,主键 `bill_id`。成本收入计提单表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `bill_id` | bigint | 计提单id |
| `batch_id` | bigint | 汇总id · 可空 |
| `source_date` | date | 来源日期 |
| `accrual_date` | date | Accrual Date · 可空 |
| `source_type` | char(3) | 计提来源类型: FI:资金对账收入 CA:成本账号 TRV:手续费收入表 TRF:手续费退款表 |
| `source_identity` | varchar(32) | 计提业务标志: 渠道编号 CA TRV TRF |
| `accrual_type` | char | 计提类型: R:收入 C:支出 |
| `accrual_account` | varchar(32) | 计提账号 |
| `detail_count` | int | 数量 · 可空 |
| `amount` | decimal(19, 4) | 金额 · 可空 |
| `currency` | char(3) | 币种 |
| `status` | char | 状态: I:初始化 R:准备完成 D:数据完成 P:归集中 F:归集失败 S:归集完成 |
| `accounting_voucher_no` | varchar(32) | 登账凭证 · 可空 |
| `extension` | varchar(255) | 扩展信息 · 可空 |
| `memo` | varchar(100) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`bill_id`
- `uk_identity_type_date`:source_identity, source_date, source_type (UNIQUE)
- `idx_batch_id`:batch_id
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

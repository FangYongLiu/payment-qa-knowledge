---
id: tbl_reconciliation_t_accrual_batch
object_type: Table
name: 成本收入计提批次表 (t_accrual_batch)
aliases: [t_accrual_batch, reconciliation.t_accrual_batch]
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

# 成本收入计提批次表 (t_accrual_batch)

## 用途
物理表 `reconciliation.t_accrual_batch`,主键 `batch_id`。成本收入计提批次表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `batch_id` | bigint | 批次id |
| `accrual_date` | date | 计提日期 |
| `accrual_type` | char | 计提类型: R:收入 C:支出 |
| `accrual_account` | varchar(32) | 计提账号 |
| `accrual_method` | char | 计提方式: A:自动 M:手动 |
| `total_amount` | decimal(19, 4) | 总金额 · 可空 |
| `currency` | char(3) | 币种 · 可空 |
| `status` | char(2) | 状态: P:处理中 WC:待确认 F:失败 S:成功 WM:待人工处理 MC:人工确认 |
| `accounting_voucher_no` | varchar(32) | 登账凭证 · 可空 |
| `report_url` | varchar(1024) | 报表地址 · 可空 |
| `extension` | varchar(255) | 扩展信息 · 可空 |
| `memo` | varchar(100) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`batch_id`
- `uk_date_type`:accrual_date, accrual_type (UNIQUE)
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

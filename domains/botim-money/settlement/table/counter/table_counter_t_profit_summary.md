---
id: tbl_counter_t_profit_summary
object_type: Table
name: 会计计提汇总 (t_profit_summary)
aliases: [t_profit_summary, counter.t_profit_summary]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: counter schema DDL
tags: [settlement, counter]
sensitivity: normal
related_services: []
---

# 会计计提汇总 (t_profit_summary)

## 用途
物理表 `counter.t_profit_summary`,主键 `flow_id`。会计计提汇总。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `flow_id` | bigint(17) | 主键 |
| `account_no` | varchar(64) | 账户编号 |
| `account_name` | varchar(255) | 账户名称 |
| `accounting_no` | varchar(64) | 会计计提账户 |
| `direction` | varchar(8) | 方向 |
| `start_date` | date | 起始日期 |
| `end_date` | date | 截止日期 |
| `amount` | decimal(15, 2) | 计提汇总金额 |
| `currency` | varchar(3) | 币种 |
| `status` | varchar(4) | 状态 |
| `message` | varchar(255) | 计提汇总信息 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `voucher_no` | varchar(64) | 登账凭证编号 · 可空 |
| `operator` | varchar(64) | 操作人员 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |
| `account_type` | varchar(4) | 账户类型 · 可空 |

## 主键 / 索引
- 主键:`flow_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_gpoint_t_account_balance
object_type: Table
name: 账户余额 (t_account_balance)
aliases: [t_account_balance, gpoint.t_account_balance]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: gpoint schema DDL
tags: [marketing, gpoint]
sensitivity: normal
related_services: []
---

# 账户余额 (t_account_balance)

## 用途
物理表 `gpoint.t_account_balance`,主键 `account_no`。账户余额。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `account_no` | bigint | 账户号：前八后九 |
| `account_type` | varchar(10) | 账户类型 |
| `account_identity` | varchar(32) | 账户标志 |
| `available_amount` | decimal(19, 2) | 可用数量 |
| `frozen_amount` | decimal(19, 2) | 冻结数量 |
| `status` | varchar(10) | 账户状态：N=正常，F=冻结 |
| `accounting_version` | bigint | 记账版本 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `create_time` | timestamp(3) | 创建时间 |
| `update_time` | timestamp(3) | 修改时间 |

## 主键 / 索引
- 主键:`account_no`
- `uk_account_type_identity`:account_identity, account_type (UNIQUE)
- `idx_create_time`:create_time
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_ccdpm_t_dpm_inner_account
object_type: Table
name: 内部账户 (t_dpm_inner_account)
aliases: [t_dpm_inner_account, ccdpm.t_dpm_inner_account]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ccdpm schema DDL
tags: [crypto, ccdpm]
sensitivity: normal
related_services: []
---

# 内部账户 (t_dpm_inner_account)

## 用途
物理表 `ccdpm.t_dpm_inner_account`,主键 `account_no`。内部账户。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `account_no` | varchar(32) | 帐号号 |
| `account_title_no` | varchar(32) | 科目号 · 可空 |
| `account_name` | varchar(100) | 账户名称 · 可空 |
| `open_date` | timestamp | 开户日期 · 可空 |
| `bal_direction` | decimal(1) | 余额方向：1:借,2:贷,0:双向 · 可空 |
| `curr_bal_direction` | decimal(1) | 当前余额方向：1:借,2:贷 · 可空 |
| `currency_code` | varchar(10) | 货币类型 · 可空 |
| `balance` | decimal(19, 8) | 余额 · 可空 |
| `accounting_version` | bigint | 记账版本 |
| `last_update_time` | timestamp | 最后更新时间 · 可空 |

## 主键 / 索引
- 主键:`account_no`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_ccdpm_t_dpm_outer_account_subset
object_type: Table
name: 外部账户分户表 (t_dpm_outer_account_subset)
aliases: [t_dpm_outer_account_subset, ccdpm.t_dpm_outer_account_subset]
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

# 外部账户分户表 (t_dpm_outer_account_subset)

## 用途
物理表 `ccdpm.t_dpm_outer_account_subset`,主键 `account_no, fund_type, balance_type`。外部账户分户表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `account_no` | varchar(32) | 账号 |
| `currency` | varchar(10) | 币种 · 可空 |
| `fund_type` | decimal(1) | 资金类型：1.借记,2.贷记 |
| `balance_type` | decimal(1) | 余额类型：1.普通,2.冻结 |
| `balance` | decimal(19, 8) | 余额 |
| `remark` | varchar(256) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`account_no, fund_type, balance_type`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

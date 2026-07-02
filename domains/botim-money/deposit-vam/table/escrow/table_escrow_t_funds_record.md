---
id: tbl_escrow_t_funds_record
object_type: Table
name: 交易报备信息表 (t_funds_record)
aliases: [t_funds_record, escrow.t_funds_record]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: escrow schema DDL
tags: [deposit-vam, escrow]
sensitivity: normal
related_services: []
---

# 交易报备信息表 (t_funds_record)

## 用途
物理表 `escrow.t_funds_record`,主键 `id`。交易报备信息表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(19) | id |
| `file_name` | varchar(255) | 文件名 · 可空 |
| `file_tag` | varchar(255) | 文件tag · 可空 |
| `dr_account` | varchar(64) | 借方账户 |
| `dr_amount` | decimal(19, 4) | 借方金额 |
| `cr_account` | varchar(64) | 贷方账户 |
| `cr_amount` | decimal(19, 4) | 贷方金额 |
| `bank_code` | varchar(64) | 银行编号，用来区分不同银行 |
| `report_time` | timestamp | 上报时间 |
| `status` | varchar(4) | 上报状态，F-ForReport待上报，R-Reported已上报，D-Dismissed已驳回 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modify` | timestamp | 更新时间 · 可空 |
| `fund_type` | varchar(4) | 调拨类型,C-CREDIT,D-DEBIT |
| `currency` | varchar(8) | 币种 |
| `batch_no` | varchar(64) | 批次编号 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

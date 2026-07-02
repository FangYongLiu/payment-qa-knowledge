---
id: tbl_npss_t_bank_file
object_type: Table
name: 银行文件表 (t_bank_file)
aliases: [t_bank_file, npss.t_bank_file]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: npss schema DDL
tags: [payment-core, npss]
sensitivity: normal
related_services: []
---

# 银行文件表 (t_bank_file)

## 用途
物理表 `npss.t_bank_file`,主键 `file_id`。银行文件表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `file_id` | bigint(19) | id |
| `file_name` | varchar(255) | 文件名 |
| `direction` | char | 方向，I-payby产生的文件,O-银行文件 |
| `file_type` | varchar(4) | 文件类型，eod-日终文件，pacs.008-交易文件,pacs.004-撤销文件，pacs.002-结果文件 |
| `file_date` | varchar(8) | 文件日期 · 可空 |
| `status` | varchar(4) | 状态 |
| `ufs_tag` | varchar(255) | ufs地址 · 可空 |
| `msg_id` | varchar(64) | 消息id · 可空 |
| `related_file_id` | bigint(19) | 原始文件id · 可空 |
| `counterpart_bic` | varchar(11) | 对方bic · 可空 |
| `total_count` | bigint(11) | 总笔数 · 可空 |
| `amount` | decimal(19, 2) | 金额 · 可空 |
| `currency` | char(3) | 币种 · 可空 |
| `extension` | varchar(255) | memo · 可空 |
| `gmt_create` | timestamp | 创建日期 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`file_id`
- `uk_file_name`:file_name (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

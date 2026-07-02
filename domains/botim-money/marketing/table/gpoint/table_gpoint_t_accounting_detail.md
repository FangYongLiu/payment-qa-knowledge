---
id: tbl_gpoint_t_accounting_detail
object_type: Table
name: 记账明细 (t_accounting_detail)
aliases: [t_accounting_detail, gpoint.t_accounting_detail]
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

# 记账明细 (t_accounting_detail)

## 用途
物理表 `gpoint.t_accounting_detail`,主键 `accounting_id`。记账明细。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `accounting_id` | bigint | 记账id：前八后九 |
| `transaction_id` | bigint | 事务ID |
| `account_no` | bigint | 账户号 |
| `accounting_type` | varchar(10) | 记账类型：O=支出，OR=退支出，I=收入，IR=退收入，F=冻结，UF=解冻，UFO=解冻支出 |
| `amount` | decimal(19, 2) | 操作数量 |
| `biz_product_code` | varchar(10) | 业务产品码 · 可空 |
| `clearing_code` | varchar(64) | 清算编码 · 可空 |
| `remark` | varchar(255) | 备注 · 可空 |
| `before_available_amount` | decimal(19, 2) | 前可用数量 |
| `before_frozen_amount` | decimal(19, 2) | 前冻结数量 |
| `after_available_amount` | decimal(19, 2) | 后可用数量 |
| `after_frozen_amount` | decimal(19, 2) | 后冻结数量 |
| `accounting_version` | bigint | 记账版本 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `create_time` | timestamp(3) | 创建时间 |

## 主键 / 索引
- 主键:`accounting_id`
- `idx_create_time_account_no`:create_time, account_no
- `idx_transaction_id`:transaction_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

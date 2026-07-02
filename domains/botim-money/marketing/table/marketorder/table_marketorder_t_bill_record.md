---
id: tbl_marketorder_t_bill_record
object_type: Table
name: 用户账单记录表 (t_bill_record)
aliases: [t_bill_record, marketorder.t_bill_record]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: marketorder schema DDL
tags: [marketing, marketorder]
sensitivity: normal
related_services: []
---

# 用户账单记录表 (t_bill_record)

## 用途
物理表 `marketorder.t_bill_record`,主键 `id`。用户账单记录表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 待补 |
| `customer_mid` | varchar(32) | 会员ID |
| `channel_code` | varchar(32) | 渠道Code |
| `account_type` | varchar(32) | 账户类型 |
| `account_number` | varchar(16) | 账户号 |
| `service_provider` | varchar(20) | 供应商 · 可空 |
| `amount` | decimal(15, 4) | 账单金额 |
| `currency` | char(3) | 币种 |
| `inputs` | varchar(64) | 供应商输入参数 · 可空 |
| `bill_due_date` | timestamp | 账单过期日 · 可空 |
| `bill_date` | timestamp | 账单产生日 |
| `notify_status` | tinyint | 是否已经通知用户 1:已通知 0:未通知 -1:不需要通知 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

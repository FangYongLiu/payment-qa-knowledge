---
id: tbl_deposit_t_payment_status_log
object_type: Table
name: 支付状态历史 (t_payment_status_log)
aliases: [t_payment_status_log, deposit.t_payment_status_log]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: deposit schema DDL
tags: [deposit-vam, deposit]
sensitivity: normal
related_services: []
---

# 支付状态历史 (t_payment_status_log)

## 用途
物理表 `deposit.t_payment_status_log`,主键 `ID`。支付状态历史。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ID` | varchar(32) | 支付状态历史ID，主键，YYYYMM+SEQ_PAYMENT_STATUS_LOG |
| `PAYMENT_VOUCHER_NO` | varchar(32) | 支付凭证号 · 可空 |
| `LAST_STATUS` | varchar(16) | 前一状态 · 可空 |
| `STATUS` | varchar(16) | 当前状态 · 可空 |
| `MEMO` | varchar(128) | 备注 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 修改时间 · 可空 |
| `LAST_SUB_STATUS` | varchar(16) | 前支付子状态 · 可空 |
| `SUB_STATUS` | varchar(16) | 当前支付子状态 · 可空 |

## 主键 / 索引
- 主键:`ID`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_payment_tb_retry_lock
object_type: Table
name: 重试锁，100行/天 (tb_retry_lock)
aliases: [tb_retry_lock, payment.tb_retry_lock]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: payment schema DDL
tags: [payment-core, payment]
sensitivity: normal
related_services: []
---

# 重试锁，100行/天 (tb_retry_lock)

## 用途
物理表 `payment.tb_retry_lock`,主键 `BIZ_TYPE, LOCK_KEY`。重试锁，100行/天。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `BIZ_TYPE` | varchar(32) | 业务类型 |
| `LOCK_KEY` | varchar(128) | 锁定主键 |
| `LOCK_STATUS` | char | 锁定状态 |
| `RETRY_COUNT` | decimal(3) | 重试次数 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFY` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`BIZ_TYPE, LOCK_KEY`
- `I_RETRY_LOCK_GMTMODIFY`:GMT_MODIFY

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

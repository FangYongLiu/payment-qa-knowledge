---
id: tbl_casheatm_t_customer_lock
object_type: Table
name: 用户锁 (t_customer_lock)
aliases: [t_customer_lock, casheatm.t_customer_lock]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: casheatm schema DDL
tags: [online-business, casheatm]
sensitivity: normal
related_services: [svc_cash_eatm]
---

# 用户锁 (t_customer_lock)

## 用途
物理表 `casheatm.t_customer_lock`,主键 `mid`。用户锁。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `mid` | varchar(200) | mid |

## 主键 / 索引
- 主键:`mid`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

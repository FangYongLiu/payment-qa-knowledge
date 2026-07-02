---
id: tbl_payment_tb_batch_payment
object_type: Table
name: 批次支付订单关系表 (tb_batch_payment)
aliases: [tb_batch_payment, payment.tb_batch_payment]
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

# 批次支付订单关系表 (tb_batch_payment)

## 用途
物理表 `payment.tb_batch_payment`,主键 `ID`。批次支付订单关系表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ID` | decimal(16) | ID主键 |
| `BATCH_SEQ_NO` | decimal(16) | 批次流水号:系统唯一 |
| `PAYMENT_ORDER_NO` | varchar(32) | 支付订单号 |
| `MARK` | varchar(32) | 批处理标记 · 可空 |
| `STATUS` | char | 处理状态 |
| `GMT_MODIFY` | timestamp | 最后修改时间 |
| `GMT_CREATE` | timestamp | 创建时间 |

## 主键 / 索引
- 主键:`ID`
- `IDX_BP_PO`:PAYMENT_ORDER_NO (UNIQUE)
- `IDX_BP_BSO`:BATCH_SEQ_NO
- `IDX_BP_MARK`:MARK

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

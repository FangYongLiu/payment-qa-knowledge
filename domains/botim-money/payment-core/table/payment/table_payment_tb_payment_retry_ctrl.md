---
id: tbl_payment_tb_payment_retry_ctrl
object_type: Table
name: 支付重试控制表 (tb_payment_retry_ctrl)
aliases: [tb_payment_retry_ctrl, payment.tb_payment_retry_ctrl]
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

# 支付重试控制表 (tb_payment_retry_ctrl)

## 用途
物理表 `payment.tb_payment_retry_ctrl`,主键 `CTRL_ID`。支付重试控制表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `CTRL_ID` | decimal(16) | ID |
| `PAYMENT_SEQ_NO` | varchar(32) | 支付流水号 |
| `STATUS` | char | 状态 |
| `BATCH_NO` | varchar(64) | 批次号 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |

## 主键 / 索引
- 主键:`CTRL_ID`
- `IDX_PRC_BATCH_NO`:BATCH_NO
- `IDX_PRC_PAYMENT_SEQ_NO`:PAYMENT_SEQ_NO
- `IDX_PRC_STATUS`:STATUS

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

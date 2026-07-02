---
id: tbl_payment_tb_biz_state_his_06
object_type: Table
name: 业务状态历史，量级同TB_BIZ_PAYMENT_ORDER (tb_biz_state_his_06)
aliases: [tb_biz_state_his_06, payment.tb_biz_state_his_06]
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

# 业务状态历史，量级同TB_BIZ_PAYMENT_ORDER (tb_biz_state_his_06)

## 用途
物理表 `payment.tb_biz_state_his_06`,主键 `HIS_ID`。业务状态历史，量级同TB_BIZ_PAYMENT_ORDER。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `HIS_ID` | decimal(18) | 历史Id |
| `BIZ_PAYMENT_SEQ_NO` | varchar(32) | 业务支付号 |
| `BIZ_SUB_STATE` | varchar(16) | 业务子状态 |
| `CUR_PAYMENT_SEQ_NO` | varchar(32) | 支付流水号 · 可空 |
| `BIZ_PAYMENT_STATE` | char | 业务状态 |
| `MEMO` | varchar(128) | 备注 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |

## 主键 / 索引
- 主键:`HIS_ID`
- `I_BIZ_STATE_HIS_BPSN_06`:BIZ_PAYMENT_SEQ_NO

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_payment_tb_payment_ctrl_08
object_type: Table
name: 支付控制指令 (tb_payment_ctrl_08)
aliases: [tb_payment_ctrl_08, payment.tb_payment_ctrl_08]
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

# 支付控制指令 (tb_payment_ctrl_08)

## 用途
物理表 `payment.tb_payment_ctrl_08`,主键 `CTRL_ID`。支付控制指令。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `CTRL_ID` | decimal(18) | SEQ:SEQ_CTRL_ORDER |
| `BIZ_PAYMENT_SEQ_NO` | varchar(32) | 业务支付订单流水号 · 可空 |
| `PAYMENT_SEQ_NO` | varchar(32) | 支付流水号 · 可空 |
| `TYPE` | varchar(16) | reject advance  支付控制：settle split payment |
| `STATE` | char | 待补 |
| `EXTENSION` | varchar(4000) | 扩展信息 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `MEMO` | varchar(256) | 备注 · 可空 |

## 主键 / 索引
- 主键:`CTRL_ID`
- `IDX_PAYMENT_CTRL_BPSN_08`:BIZ_PAYMENT_SEQ_NO
- `IDX_PAYMENT_CTRL_PSN_08`:PAYMENT_SEQ_NO
- `I_PAYMENT_CTRL_GMT_MOD_08`:GMT_MODIFIED

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

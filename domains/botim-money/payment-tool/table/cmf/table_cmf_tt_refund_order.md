---
id: tbl_cmf_tt_refund_order
object_type: Table
name: 退款订单 (tt_refund_order)
aliases: [tt_refund_order, cmf.tt_refund_order]
domain: payment-tool
status: active
owner: kingo.liang
reviewer: kingo.liang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cmf schema DDL
tags: [payment-tool, cmf]
sensitivity: normal
related_services: []
---

# 退款订单 (tt_refund_order)

## 用途
物理表 `cmf.tt_refund_order`,主键 `INST_ORDER_ID`。退款订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `INST_ORDER_ID` | decimal(19) | 机构订单ID |
| `FUNDIN_ORDER_NO` | varchar(32) | 充值订单号 |
| `FUNDIN_REAL_AMOUNT` | decimal(15, 2) | 充值实收金额 · 可空 |
| `CURRENCY` | char(3) | 币种 · 可空 |
| `FUNDIN_DATE` | varchar(16) | 入款时间 · 可空 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |

## 主键 / 索引
- 主键:`INST_ORDER_ID`
- `IX_TTREFUNDORDER_GMTMD`:GMT_MODIFIED

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

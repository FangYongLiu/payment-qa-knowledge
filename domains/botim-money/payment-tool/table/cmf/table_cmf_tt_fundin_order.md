---
id: tbl_cmf_tt_fundin_order
object_type: Table
name: 入款订单 (tt_fundin_order)
aliases: [tt_fundin_order, cmf.tt_fundin_order]
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

# 入款订单 (tt_fundin_order)

## 用途
物理表 `cmf.tt_fundin_order`,主键 `INST_ORDER_ID`。入款订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `INST_ORDER_ID` | decimal(19) | 机构订单ID |
| `CARD_TYPE` | varchar(8) | 卡类型：CC:贷记卡,DC:借记卡,SCC:准借记卡,PB:存折 · 可空 |
| `PAYER_INST_CODE` | varchar(16) | 付款机构 · 可空 |
| `CONTRACT_NO` | varchar(64) | 协议号,用于一点充 · 可空 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `GMT_CREATED` | timestamp | 创建时间 · 可空 |

## 主键 / 索引
- 主键:`INST_ORDER_ID`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

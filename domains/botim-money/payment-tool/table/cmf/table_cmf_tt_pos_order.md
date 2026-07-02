---
id: tbl_cmf_tt_pos_order
object_type: Table
name: POS订单 (tt_pos_order)
aliases: [tt_pos_order, cmf.tt_pos_order]
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

# POS订单 (tt_pos_order)

## 用途
物理表 `cmf.tt_pos_order`,主键 `ORDER_ID`。POS订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ORDER_ID` | decimal(11) | 订单ID |
| `BATCH_ID` | decimal(11) | 批次ID |
| `REQUEST_NO` | varchar(32) | 请求号 |
| `API_TYPE` | varchar(8) | API类型 |
| `INST_ORDER_NO` | varchar(32) | 机构订单号 |
| `PRE_INST_ORDER_NO` | varchar(32) | 原机构订单号 · 可空 |
| `INST_SEQ_NO` | varchar(32) | 机构流水号 · 可空 |
| `AMOUNT` | decimal(15, 2) | 金额 · 可空 |
| `REAL_AMOUNT` | decimal(15, 2) | 实付金额 · 可空 |
| `CURRENCY` | char(3) | 币种 · 可空 |
| `STATUS` | char | 状态 |
| `SUBMIT_BATCH_NO` | decimal(11) | 上送批次号 · 可空 |
| `SUBMIT_INST_NO` | varchar(32) | 上送机构订单号 · 可空 |
| `SETTLEMENT_DATE` | char(8) | 结算日期 · 可空 |
| `EXTENSION` | varchar(2048) | 扩展信息 · 可空 |
| `ROUTE_VERSION` | decimal(8) | 路由版本 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |
| `RETRY_STATUS` | char | F,失败;S,成功;A,等待; · 可空 |

## 主键 / 索引
- 主键:`ORDER_ID`
- `UIDX_PO_AT_RN`:API_TYPE, REQUEST_NO (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

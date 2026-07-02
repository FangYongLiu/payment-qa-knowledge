---
id: tbl_cmf_tt_control_order_result
object_type: Table
name: tt_control_order_result (tt_control_order_result)
aliases: [tt_control_order_result, cmf.tt_control_order_result]
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

# tt_control_order_result (tt_control_order_result)

## 用途
物理表 `cmf.tt_control_order_result`,主键 `RESULT_ID`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `RESULT_ID` | decimal(19) | 结果ID |
| `CONTROL_ORDER_ID` | decimal(19) | 流水号 · 可空 |
| `AMOUNT` | decimal(18, 2) | 金额 · 可空 |
| `CURRENCY` | char(3) | 币种 · 可空 |
| `INST_ORDER_NO` | varchar(32) | 机构订单号 · 可空 |
| `INST_RESULT_CODE` | varchar(32) | 统一返回码 · 可空 |
| `API_TYPE` | varchar(16) | API类型 · 可空 |
| `STATUS` | char | 状态 · 可空 |
| `API_RESULT_CODE` | varchar(32) | API结果编码 · 可空 |
| `API_SUB_RESULT_CODE` | varchar(32) | API结果子码 · 可空 |
| `RESULT_MESSAGE` | varchar(256) | 结果信息 · 可空 |
| `MEMO` | varchar(256) | 备注 · 可空 |
| `EXTENSION` | varchar(2048) | 扩展信息 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 · 可空 |
| `GMT_MODIFIED` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`RESULT_ID`
- `IX_TTCONTROLRESULT_GMTCREATE`:GMT_CREATE
- `IX_TTCONTROLRESULT_INSTORDERNO`:INST_ORDER_NO
- `IX_TTCONTROLRESULT_ORDERID`:CONTROL_ORDER_ID

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

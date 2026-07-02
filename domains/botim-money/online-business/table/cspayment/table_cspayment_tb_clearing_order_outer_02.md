---
id: tbl_cspayment_tb_clearing_order_outer_02
object_type: Table
name: 清算指令外场 (tb_clearing_order_outer_02)
aliases: [tb_clearing_order_outer_02, cspayment.tb_clearing_order_outer_02]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cspayment schema DDL
tags: [online-business, cspayment]
sensitivity: normal
related_services: []
---

# 清算指令外场 (tb_clearing_order_outer_02)

## 用途
物理表 `cspayment.tb_clearing_order_outer_02`,主键 `CLEARING_ORDER_ID`。清算指令外场。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `CLEARING_ORDER_ID` | decimal(18) | 主键，SEQ_CLEARING_ORDER |
| `REQUEST_NO` | varchar(32) | 请求号 |
| `PARTY_ROLE` | varchar(16) | 参与角色 |
| `PARTY_ID` | varchar(64) | 参与方ID · 可空 |
| `CURRENCY` | char(3) | 币种 |
| `AMOUNT` | decimal(15, 4) | 金额 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |
| `CLEARING_CODE` | varchar(32) | 清算编码 · 可空 |

## 主键 / 索引
- 主键:`CLEARING_ORDER_ID`
- `IDX_COO_REQUEST_NO_02`:REQUEST_NO

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

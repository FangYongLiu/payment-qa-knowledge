---
id: tbl_cmf_tt_control_order
object_type: Table
name: tt_control_order (tt_control_order)
aliases: [tt_control_order, cmf.tt_control_order]
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

# tt_control_order (tt_control_order)

## 用途
物理表 `cmf.tt_control_order`,主键 `ORDER_ID`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ORDER_ID` | decimal(19) | 流水号 |
| `FUND_CHANNEL_CODE` | varchar(32) | 资金渠道编码 · 可空 |
| `PAY_MODE` | varchar(32) | 支付方式 · 可空 |
| `INST_CODE` | varchar(32) | 机构编码 · 可空 |
| `PRODUCT_CODE` | varchar(32) | 产品编码 · 可空 |
| `REQUEST_NO` | varchar(32) | 请求号 |
| `REQUEST_TYPE` | varchar(8) | 请求类型 |
| `API_TYPE` | varchar(16) | API类型 · 可空 |
| `INST_ORDER_NO` | varchar(32) | 机构订单号 · 可空 |
| `PRE_REQUEST_NO` | varchar(32) | 原请求号 · 可空 |
| `AMOUNT` | decimal(15, 2) | 金额 · 可空 |
| `CURRENCY` | char(3) | 币种 · 可空 |
| `STATUS` | char | 状态 · 可空 |
| `RETRY_STATUS` | char | F,失败;S,成功;A,等待; · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 · 可空 |
| `GMT_MODIFIED` | timestamp | 修改时间 · 可空 |
| `EXTENSION` | varchar(2048) | 扩展信息 · 可空 |
| `MEMO` | varchar(128) | 备注 · 可空 |
| `NOTIFY_STATUS` | char | 通知前端MAS,PE结果状态 · 可空 |
| `SOURCE_CODE` | varchar(16) | MAS,PE · 可空 |
| `COMMUNICATE_STATUS` | char | 通讯状态，类型为单笔时：A（等待指令发送），S（指令已经发送），R（数据已经返回），F（指令发送失败）。 · 可空 |
| `FLAG` | char | 用于订单做查询类操作时临时更新标志使用 · 可空 |
| `MERCHANT_ID` | varchar(32) | 商户id · 可空 |
| `GMT_NEXT_RETRY` | timestamp | 下次重试时间 · 可空 |
| `RETRY_TIMES` | decimal(6) | 补单次数 · 可空 |

## 主键 / 索引
- 主键:`ORDER_ID`
- `IX_TTCONTROLORDER_GMTCREATE`:GMT_CREATE
- `IX_TTCONTROLORDER_INSTORDERNO`:INST_ORDER_NO
- `IX_TTCONTROLORDER_PREREQUESTNO`:PRE_REQUEST_NO
- `IX_TTCONTROLORDER_REQUESTNO`:REQUEST_NO

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

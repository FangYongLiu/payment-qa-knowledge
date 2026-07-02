---
id: tbl_cmf_tt_cmf_request
object_type: Table
name: CMF请求表，用于控制唯一 (tt_cmf_request)
aliases: [tt_cmf_request, cmf.tt_cmf_request]
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

# CMF请求表，用于控制唯一 (tt_cmf_request)

## 用途
物理表 `cmf.tt_cmf_request`,主键 `PAYMENT_SEQ_NO, SETTLEMENT_ID`。CMF请求表，用于控制唯一。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `PAYMENT_SEQ_NO` | varchar(32) | 支付流水号 |
| `CAN_RETRY` | char | 是否允许重试：Y（是），N（否） |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `SETTLEMENT_ID` | varchar(32) | 结算id |

## 主键 / 索引
- 主键:`PAYMENT_SEQ_NO, SETTLEMENT_ID`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

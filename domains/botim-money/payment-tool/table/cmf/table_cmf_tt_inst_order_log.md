---
id: tbl_cmf_tt_inst_order_log
object_type: Table
name: 废除日志表 (tt_inst_order_log)
aliases: [tt_inst_order_log, cmf.tt_inst_order_log]
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

# 废除日志表 (tt_inst_order_log)

## 用途
物理表 `cmf.tt_inst_order_log`,主键 `LOG_ID`。废除日志表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `LOG_ID` | decimal(15) | 日志ID |
| `INST_ORDER_ID` | decimal(15) | 机构订单ID |
| `INST_ORDER_NO` | varchar(32) | 机构订单号 |
| `CMF_SEQ_NO` | varchar(32) | 渠道流水号，yyyymmdd+seq_cmf_order |
| `ORDER_INFO` | varchar(3072) | 订单信息 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |

## 主键 / 索引
- 主键:`LOG_ID`
- `IX_TTINSTORDERLOG_CMFSEQNO`:CMF_SEQ_NO
- `IX_TTINSTORDERLOG_GMTCREATE`:GMT_CREATE
- `IX_TTINSTORDERLOG_INSTORDERID`:INST_ORDER_ID
- `IX_TTINSTORDERLOG_INSTORDERNO`:INST_ORDER_NO

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

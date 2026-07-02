---
id: tbl_cmf_tt_order_submit_history
object_type: Table
name: 订单提交历史 (tt_order_submit_history)
aliases: [tt_order_submit_history, cmf.tt_order_submit_history]
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

# 订单提交历史 (tt_order_submit_history)

## 用途
物理表 `cmf.tt_order_submit_history`,主键 `SUBMIT_HISTORY_ID`。订单提交历史。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `SUBMIT_HISTORY_ID` | decimal(15) | 提交历史ID |
| `CMF_SEQ_NO` | varchar(32) | 渠道流水号 |
| `INST_ORDER_ID` | decimal(15) | 机构订单ID |
| `GMT_CREATE` | timestamp | 创建时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |

## 主键 / 索引
- 主键:`SUBMIT_HISTORY_ID`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

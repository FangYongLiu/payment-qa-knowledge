---
id: tbl_cmf_tt_payment_notify_log
object_type: Table
name: 支付结果通知日志 (tt_payment_notify_log)
aliases: [tt_payment_notify_log, cmf.tt_payment_notify_log]
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

# 支付结果通知日志 (tt_payment_notify_log)

## 用途
物理表 `cmf.tt_payment_notify_log`,主键 `NOTIFY_LOG_ID`。支付结果通知日志。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `NOTIFY_LOG_ID` | decimal(19) | 通知日志ID |
| `CHANNEL_SEQ_NO` | varchar(32) | 渠道流水号 |
| `NOTIFY_RESULT` | char | 通知结果：S（成功），F（失败） |
| `GMT_CREATE` | timestamp | 创建时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |

## 主键 / 索引
- 主键:`NOTIFY_LOG_ID`
- `IDX_PAYMENTNOTIFYLOG`:CHANNEL_SEQ_NO

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

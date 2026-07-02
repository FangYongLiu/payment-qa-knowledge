---
id: tbl_cmf_tl_event_notify_log
object_type: Table
name: tl_event_notify_log (tl_event_notify_log)
aliases: [tl_event_notify_log, cmf.tl_event_notify_log]
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

# tl_event_notify_log (tl_event_notify_log)

## 用途
物理表 `cmf.tl_event_notify_log`,主键 `NOTIFY_ID`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `NOTIFY_ID` | decimal(11) | 通知ID |
| `EVENT` | char(2) | 事件 · 可空 |
| `PROTOCOL` | varchar(20) | 协议 |
| `TARGET_ADDRESS` | varchar(200) | 目标地址 |
| `MAX_RETRY_TIMES` | decimal(2) | 最大重试时间 · 可空 |
| `RETRY_TIMES` | decimal(2) | 重试时间 · 可空 |
| `NOTIFY_BODY` | varchar(2000) | 通知内容 · 可空 |
| `NOTIFY_STATUS` | char | F-失败,S-成功,P-发送中 · 可空 |
| `MEMO` | varchar(128) | 备忘录 · 可空 |
| `GMT_CREATED` | timestamp | 创建时间 · 可空 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 · 可空 |

## 主键 / 索引
- 主键:`NOTIFY_ID`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

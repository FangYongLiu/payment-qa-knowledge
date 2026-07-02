---
id: tbl_cmf_tm_work_date
object_type: Table
name: 事件通知记录，目前只记录失败的消息 (tm_work_date)
aliases: [tm_work_date, cmf.tm_work_date]
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

# 事件通知记录，目前只记录失败的消息 (tm_work_date)

## 用途
物理表 `cmf.tm_work_date`,主键 `DATE_STRING`。事件通知记录，目前只记录失败的消息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `DATE_STRING` | char(8) | 日期字符串，yyyymmdd |
| `WORK_FLAG` | char | 工作日标记，Y:工作日，N:非工作日 · 可空 |
| `OPERATOR` | varchar(64) | 操作员 |
| `MEMO` | varchar(256) | 备注 · 可空 |
| `GMT_CREATED` | timestamp | 创建时间 · 可空 |
| `GMT_MODIFIED` | timestamp | 最后发送时间 · 可空 |

## 主键 / 索引
- 主键:`DATE_STRING`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

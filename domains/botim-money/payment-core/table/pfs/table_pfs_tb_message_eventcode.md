---
id: tbl_pfs_tb_message_eventcode
object_type: Table
name: 稳定，100行 (tb_message_eventcode)
aliases: [tb_message_eventcode, pfs.tb_message_eventcode]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: pfs schema DDL
tags: [payment-core, pfs]
sensitivity: normal
related_services: []
---

# 稳定，100行 (tb_message_eventcode)

## 用途
物理表 `pfs.tb_message_eventcode`,主键 `EVENT_CODE_ID`。稳定，100行。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `EVENT_CODE_ID` | decimal(15) | 待补 |
| `EVENT_CODE` | varchar(256) | 事件编码 |
| `EVENT_NAME` | varchar(256) | 事件名称 |
| `MATCH_EVENT_TYPE` | varchar(128) | 匹配事件类型 |
| `MATCH_EXPRESSION` | varchar(2000) | 事件匹配表达式 |
| `EXTENSIONS` | varchar(512) | 扩展信息 · 可空 |
| `ENABLE_FLAG` | char | 启用标识 |
| `MEMO` | varchar(256) | 备注 · 可空 |
| `OPERATOR` | varchar(128) | 操作员 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFY` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`EVENT_CODE_ID`
- `UK_MESSAGE_EVENTCODE_EVENTCODE`:EVENT_CODE (UNIQUE)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

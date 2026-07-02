---
id: tbl_pns_t_partner_notify_log
object_type: Table
name: 同T_PARTNER_NOTIFY数量级 (t_partner_notify_log)
aliases: [t_partner_notify_log, pns.t_partner_notify_log]
domain: infrastructure
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: pns schema DDL
tags: [infrastructure, pns]
sensitivity: normal
related_services: []
---

# 同T_PARTNER_NOTIFY数量级 (t_partner_notify_log)

## 用途
物理表 `pns.t_partner_notify_log`,主键 `NOTIFY_REQUEST_ID`。同T_PARTNER_NOTIFY数量级。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `NOTIFY_REQUEST_ID` | decimal(18) | 通知请求ID |
| `NOTIFY_ID` | decimal(18) | 通知ID |
| `NOTIFY_RETURN_DATA` | varchar(512) | 通知返回数据 · 可空 |
| `SERVER_IDENTITY` | varchar(16) | 待补 |
| `GMT_NOTIFY` | timestamp | 创建时间 |
| `GMT_RETURN` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`NOTIFY_REQUEST_ID`
- `I_PARTNER_NOTIFY_LOG_NOTIFYID`:NOTIFY_ID

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

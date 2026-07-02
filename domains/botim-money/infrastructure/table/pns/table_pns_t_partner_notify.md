---
id: tbl_pns_t_partner_notify
object_type: Table
name: 业务号 (t_partner_notify)
aliases: [t_partner_notify, pns.t_partner_notify]
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

# 业务号 (t_partner_notify)

## 用途
物理表 `pns.t_partner_notify`,主键 `NOTIFY_ID`。业务号。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `NOTIFY_ID` | decimal(18) | 通知ID |
| `VOUCHER_NO` | varchar | 待补 · 可空 |

## 主键 / 索引
- 主键:`NOTIFY_ID`
- `I_PARTNER_NOTIFY_GMT_CREATE`:GMT_CREATE
- `I_PARTNER_NOTIFY_GMT_RETRY`:GMT_RETRY
- `I_PARTNER_NOTIFY_RETRY`:PARTNER_TYPE, NOTIFY_STATUS, RETRYING_FLAG, GMT_RETRY

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

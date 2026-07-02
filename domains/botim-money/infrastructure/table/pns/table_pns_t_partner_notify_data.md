---
id: tbl_pns_t_partner_notify_data
object_type: Table
name: 商户通知内容 (t_partner_notify_data)
aliases: [t_partner_notify_data, pns.t_partner_notify_data]
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

# 商户通知内容 (t_partner_notify_data)

## 用途
物理表 `pns.t_partner_notify_data`,主键 `NOTIFY_DATA_ID`。商户通知内容。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `NOTIFY_DATA_ID` | decimal(18) | 内容ID格式：8位日期+9位序列+1业务码 |
| `NOTIFY_ID` | decimal(18) | 通知ID |
| `DATA_TYPE` | varchar(32) | 内容类型:批量BATCH,单笔SIMPLE |
| `NOTIFY_CONTENT` | varchar(4000) | 内容 · 可空 |
| `SORT` | decimal(9) | 排序 · 可空 |

## 主键 / 索引
- 主键:`NOTIFY_DATA_ID`
- `I_PARTNER_NOTIFY_D_NOTIFYID`:NOTIFY_ID

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

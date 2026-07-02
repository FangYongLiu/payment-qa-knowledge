---
id: tbl_pns_t_partner_notify
object_type: Table
name: 同交易订单数量级 (t_partner_notify)
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

# 同交易订单数量级 (t_partner_notify)

## 用途
物理表 `pns.t_partner_notify`,主键 `NOTIFY_ID`。同交易订单数量级。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `NOTIFY_ID` | decimal(18) | 通知ID |
| `VOUCHER_NO` | varchar(64) | 业务号 |
| `EVENT_CODE` | varchar(32) | 通知事件编码 |
| `NOTIFY_TARGET` | varchar(400) | 通知地址 |
| `NOTIFY_STATUS` | varchar(16) | 通知状态 |
| `INPUT_CHARSET` | varchar(64) | 字符集编码 |
| `SIGNATURE_TYPE` | varchar(16) | 签名类型 |
| `PARTNER_ID` | varchar(100) | 合作方ID |
| `CLIENT_ID` | varchar(32) | 客户端ID |
| `SERVER_IDENTITY` | varchar(16) | 服务器标识 |
| `RETRYING_FLAG` | char | 待补 |
| `RETRY_COUNT` | decimal(2) | 通知次数 |
| `GMT_RETRY` | timestamp | 重试时间 · 可空 |
| `MEMO` | varchar(256) | 系统备注 · 可空 |
| `group_name` | varchar(200) | 集团名称 · 可空 |
| `branch_name` | varchar(200) | 分支名称 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 修改时间 |
| `BATCH_FLAG` | varchar(1) | 是否批量通知 · 可空 |
| `PARTNER_TYPE` | varchar(64) | Partner type (retry job partition key) · 可空 |

## 主键 / 索引
- 主键:`NOTIFY_ID`
- `UK_PARTNER_NOTIFY_BUSINESSKEY`:VOUCHER_NO, EVENT_CODE, PARTNER_ID (UNIQUE)
- `I_PARTNER_NOTIFY_GMT_CREATE`:GMT_CREATE
- `I_PARTNER_NOTIFY_GMT_RETRY`:GMT_RETRY
- `I_PARTNER_NOTIFY_RETRY`:PARTNER_TYPE, NOTIFY_STATUS, RETRYING_FLAG, GMT_RETRY

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_npss_t_recent_contact
object_type: Table
name: 最近联系人唯一索引 (t_recent_contact)
aliases: [t_recent_contact, npss.t_recent_contact]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: npss schema DDL
tags: [payment-core, npss]
sensitivity: normal
related_services: []
---

# 最近联系人唯一索引 (t_recent_contact)

## 用途
物理表 `npss.t_recent_contact`,主键 `contact_id`。最近联系人唯一索引。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `contact_id` | bigint(18) | 主键 · 可空 |
| `sender_id` | varchar(20) | 发送人mid |
| `business_type` | varchar(15) | 业务类型(SEND_MONEY,REQUEST_TO_PAY,SPLIT_BILL) |
| `recipient_type` | varchar(10) | 接收类型,mobile-手机,eid-身份证,email-邮箱 |
| `recipient_name` | varchar(30) | 接受人姓名(掩码) · 可空 |
| `recipient_account_val` | varchar(20) | 账户号 |
| `memo` | varchar(100) | 备注 · 可空 |
| `last_trans_amount` | decimal(19, 4) | Last Trans Amount · 可空 |
| `currency` | char(3) | Currency · 可空 |
| `last_trans_time` | timestamp | 最近交易时间 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`contact_id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_rtp_t_refund_order
object_type: Table
name: Refund Order (t_refund_order)
aliases: [t_refund_order, rtp.t_refund_order]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: rtp schema DDL
tags: [online-business, rtp]
sensitivity: normal
related_services: []
---

# Refund Order (t_refund_order)

## 用途
物理表 `rtp.t_refund_order`,主键 `refund_order_no`。Refund Order。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `refund_order_no` | bigint | Refund Order No: voucher no |
| `payee_order_no` | bigint | Payee Order No · 可空 |
| `payer_order_no` | bigint | Payer Order No |
| `rtp_method` | varchar(10) | Rtp Method: BOTIM/AANI |
| `amount` | decimal(19, 4) | Amount |
| `currency` | char(3) | Currency |
| `reason` | varchar(150) | Reason · 可空 |
| `status` | varchar(10) | Status |
| `unity_result_code` | varchar(50) | Unity Result Code · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `create_time` | timestamp | Create Time |
| `update_time` | timestamp | Update Time |
| `finish_time` | timestamp | Finish Time · 可空 |

## 主键 / 索引
- 主键:`refund_order_no`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_rtp_t_relate_trade_order
object_type: Table
name: Relate Trade Order (t_relate_trade_order)
aliases: [t_relate_trade_order, rtp.t_relate_trade_order]
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

# Relate Trade Order (t_relate_trade_order)

## 用途
物理表 `rtp.t_relate_trade_order`,主键 `trade_request_no`。Relate Trade Order。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `trade_request_no` | bigint | Trade Request No |
| `order_type` | varchar(10) | Order Type: R_C=Pay Relation Cancel, PAYER_C=Payer Order Cancel, PAYEE_S=Payee Order Settle, PAYER_S=Payer Order Settle |
| `order_voucher_no` | bigint | Order Voucher No |
| `order_status` | char | Order Status: P-Processing, F-Fail, S-Success |
| `extension` | varchar(255) | Extension · 可空 |
| `create_time` | timestamp | Create Time |
| `update_time` | timestamp | Update Time |

## 主键 / 索引
- 主键:`trade_request_no`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

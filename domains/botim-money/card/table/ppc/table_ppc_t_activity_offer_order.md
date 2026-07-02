---
id: tbl_ppc_t_activity_offer_order
object_type: Table
name: Activity Offer Order (t_activity_offer_order)
aliases: [t_activity_offer_order, ppc.t_activity_offer_order]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ppc schema DDL
tags: [card, ppc]
sensitivity: normal
related_services: []
---

# Activity Offer Order (t_activity_offer_order)

## 用途
物理表 `ppc.t_activity_offer_order`,主键 `voucher_no`。Activity Offer Order。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `voucher_no` | bigint | Order Voucher No |
| `offer_type` | varchar(10) | Offer Type: APC_ZP=Apply Physical Card Zero Pay |
| `request_no` | varchar(64) | Request No |
| `client_id` | varchar(32) | Client ID |
| `payer_id` | varchar(20) | Payer ID |
| `pay_amount` | decimal(19, 4) | Pay Amount |
| `refund_amount` | decimal(19, 4) | Refund Amount · 可空 |
| `currency` | char(3) | Currency |
| `status` | varchar(2) | Status: W=Wait Pay,P=Paid,CO=Closed,RI=Refunding,R=Refunded,CP=Completed |
| `refund_request_no` | bigint | Refund Request No · 可空 |
| `payer_partner_id` | varchar(20) | Payer Partner ID: Botim/PayBy Partner ID |
| `payee_member_id` | varchar(20) | Payee Member ID |
| `expire_time` | timestamp | Expire Time |
| `paid_time` | timestamp | Paid Time · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `update_time` | timestamp | Update time |
| `create_time` | timestamp | Create time |

## 主键 / 索引
- 主键:`voucher_no`
- `idx_expire_time`:expire_time
- `idx_paid_time`:paid_time
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

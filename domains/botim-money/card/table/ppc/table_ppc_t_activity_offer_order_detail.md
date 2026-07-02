---
id: tbl_ppc_t_activity_offer_order_detail
object_type: Table
name: Activity Offer Order Detail (t_activity_offer_order_detail)
aliases: [t_activity_offer_order_detail, ppc.t_activity_offer_order_detail]
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

# Activity Offer Order Detail (t_activity_offer_order_detail)

## 用途
物理表 `ppc.t_activity_offer_order_detail`,主键 `offer_detail_id`。Activity Offer Order Detail。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `offer_detail_id` | bigint | Offer Detail ID |
| `offer_order_voucher_no` | bigint | Offer Order Voucher No |
| `member_id` | varchar(20) | Member ID |
| `value_amount` | decimal(19, 4) | Value Amount |
| `currency` | char(3) | Currency |
| `activity_offer_id` | bigint | Activity Offer ID · 可空 |
| `offer_extension` | varchar(255) | Offer Extension: physicalCardType · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`offer_detail_id`
- `idx_offer_voucher_no`:offer_order_voucher_no
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

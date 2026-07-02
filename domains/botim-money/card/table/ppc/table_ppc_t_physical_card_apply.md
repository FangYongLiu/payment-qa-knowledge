---
id: tbl_ppc_t_physical_card_apply
object_type: Table
name: Physical Card Apply (t_physical_card_apply)
aliases: [t_physical_card_apply, ppc.t_physical_card_apply]
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

# Physical Card Apply (t_physical_card_apply)

## 用途
物理表 `ppc.t_physical_card_apply`,主键 `apply_id`。Physical Card Apply。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `apply_id` | bigint | ID, 前八后九 |
| `virtual_card_id` | bigint | Card ID |
| `delivery_id` | bigint | Delivery ID · 可空 |
| `delivery_type` | char(3) | Delivery Type: C=Cash, COD=Cash on Delivery |
| `fee_request_no` | bigint | Fee Request No · 可空 |
| `status` | char | Apply Status: C=Created, P=Processing, M=MakingCard, D=DeliveryCancelled, S=SignOnDelivered, A=Activated, F=Pay Fail/Order Closed/Manually Cancelled |
| `sub_status` | char(2) | Sub status: RD=Ready to Delivery, IT=In Transit · 可空 |
| `name_on_card` | varchar(32) | Name On Card: Ues Encrypt · 可空 |
| `paid_time` | timestamp(3) | Paid Time · 可空 |
| `shipping_time` | timestamp | Shipping Time · 可空 |
| `delivered_time` | timestamp | Delivered Time · 可空 |
| `trx_ref_no` | varchar(12) | Transaction Ref No: Processor associate · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `create_time` | timestamp(3) | Create time |
| `update_time` | timestamp(3) | Update time |
| `physical_card_type` | char | Physical Card Type |

## 主键 / 索引
- 主键:`apply_id`
- `idx_delivered_time`:delivered_time
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

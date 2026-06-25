---
id: tbl_acquireii_t_fiserv_refund_bucket
object_type: Table
name: Fiserv 退款资金桶表 (t_fiserv_refund_bucket)
aliases: [t_fiserv_refund_bucket, fiserv退款资金桶]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: DB 文档
source_ref: tables/t_fiserv_refund_bucket.md
tags: [online-business, 收单, fiserv, refund, 退款]
related_services: [svc_acquireii]
related_scenarios: [scn_online_business_transaction_db_check]
---

# Fiserv 退款资金桶表 (t_fiserv_refund_bucket)

## 用途
记录一笔 Fiserv 订单的**退款额度池**,管理三态金额:可退款 (refundable)、退款中 (refunding)、已退款 (refunded)。物理表 `acquireii.t_fiserv_refund_bucket`,主键 `global_id`,对应订单 global_id。属收单服务 [[svc_acquireii]],在 Fiserv/POS 退款流程中读写。

**典型流转**(以 1000 订单为例):
- 初始:refundable=1000, refunding=0, refunded=0
- 发起退款 300:refunding=300, refundable=700
- 退款成功:refunded=300, refunding=0, refundable=700
- 再退 200:refunded=500, refundable=500
- 退款失败:refunding → refundable 回退

## 关联关系
- **所属服务**:[[svc_acquireii]](= `related_services`,tbl→service 边)。
- **谁读写它**:收单/退款链路服务与接口(由对方 `related_tables` 声明)。退款主单 [[tbl_acquireii_t_refund_order]] 与本桶按 origin global_id 关联;Fiserv 销售主单 `t_fiserv_sale_order`(对象待补)1:1 关联 global_id。
- **哪些场景校验它**:[[scn_online_business_transaction_db_check]](= `related_scenarios`,商户交易落库检查)。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| global_id | bigint | 主键,对应订单 global_id |
| refundable_currency_code | varchar(50) | 可退款币种 |
| refundable_amount | decimal(19,4) | 还能退多少(剩余可退) |
| refunding_currency_code | varchar(50) | 退款中币种 |
| refunding_amount | decimal(19,4) | 处理中金额 |
| refunded_currency_code | varchar(50) | 已退款币种 |
| refunded_amount | decimal(19,4) | 已成功退款金额 |
| created_time | timestamp(3) | 创建时间 |
| last_updated_time | timestamp(3) | 最后更新时间 |
| data_version | bigint | 乐观锁版本号 |

## 主键 / 索引
- 主键:`global_id`
- 索引:`i_frb_ct`(created_time,按创建时间查询)、`i_frb_lut`(last_updated_time,按更新时间查询)
- 关联:1:1 → `t_fiserv_sale_order`(global_id);1:N → `t_fiserv_refund_order`(origin_global_id → global_id)。这两张 Fiserv 表对象待补。

## 校验点(QA 关注)
- **三态金额平衡**:`refundable_amount + refunding_amount + refunded_amount = 原订单金额`,误差 < 0.01,可 JOIN `t_fiserv_sale_order` 校验。
- **乐观锁**:更新必须带 `data_version`,并发下防覆盖。
- **退款失败回退**:退款失败时 `refunding_amount` 回退到 `refundable_amount`,不可残留 refunding 态。
- **多次退款共用 bucket**:同一 global_id 的 bucket 唯一,多次退款经 `t_fiserv_refund_order.origin_global_id` 关联,bucket 只增量更新。
- **净可退计算**:实际可发起退款 = `refundable_amount - refunding_amount`,避免重复发起超额退款。
- **币种一致性**:三个 currency_code 应与原订单币种一致。

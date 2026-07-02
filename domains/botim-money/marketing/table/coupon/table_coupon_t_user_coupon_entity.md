---
id: tbl_coupon_t_user_coupon_entity
object_type: Table
name: t_user_coupon_entity (t_user_coupon_entity)
aliases: [t_user_coupon_entity, coupon.t_user_coupon_entity]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: coupon schema DDL
tags: [marketing, coupon]
sensitivity: normal
related_services: []
---

# t_user_coupon_entity (t_user_coupon_entity)

## 用途
物理表 `coupon.t_user_coupon_entity`,主键 `entity_id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `entity_id` | bigint | 主键 |
| `request_no` | varchar(64) | 请求号 |
| `member_id` | varchar(32) | 用户id |
| `coupon_id` | bigint | 券id · 可空 |
| `coupon_code` | varchar(32) | 券码 |
| `coupon_detail_id` | bigint | 券码表id · 可空 |
| `campaign_id` | bigint | 活动id · 可空 |
| `status` | varchar(32) | 状态 |
| `received_type` | varchar(32) | marketing营销系统发放|coupon系统发放 · 可空 |
| `partner_id` | varchar(32) | 来源 |
| `merchant_id` | bigint | 商户id · 可空 |
| `supplier_id` | bigint | 券来源 · 可空 |
| `created_time` | timestamp | 领取时间 |
| `updated_time` | timestamp | 修改时间 |
| `writeoff_time` | timestamp | 核销时间 · 可空 |
| `backoff_time` | timestamp | 回退时间（当有资金流的时候需要记录） · 可空 |
| `recovery_time` | timestamp | 回收（人工失效需要用到） · 可空 |
| `effective_time` | timestamp | 生效时间 · 可空 |
| `expired_time` | timestamp | 过期时间 · 可空 |
| `coupon_type` | varchar(32) | 券类型，兑换券-GIFT，代金券-CASH，满减券-CUT，折扣券-DISCOUNT · 可空 |
| `coupon_source` | varchar(32) | 券来源 · 可空 |
| `discount_amount` | decimal(19, 4) | 优惠金额 · 可空 |
| `currency` | char(3) | 币种 · 可空 |
| `face_value` | decimal(19, 4) | 面额 · 可空 |
| `record_id` | bigint | 记录订单id · 可空 |

## 主键 / 索引
- 主键:`entity_id`
- `idx_couponDetailId`:coupon_detail_id
- `idx_member_id`:member_id
- `idx_record_id`:record_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_scoupon_t_user_chance_detail
object_type: Table
name: 用户机会表 (t_user_chance_detail)
aliases: [t_user_chance_detail, scoupon.t_user_chance_detail]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: scoupon schema DDL
tags: [marketing, scoupon]
sensitivity: normal
related_services: []
---

# 用户机会表 (t_user_chance_detail)

## 用途
物理表 `scoupon.t_user_chance_detail`,主键 `id`。用户机会表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 |
| `member_id` | varchar(32) | 用户id |
| `source` | varchar(32) | 机会来源 kyc,nokyc,share, monthly |
| `chances` | int | 机会次数 |
| `notify_flag` | varchar(32) | 通知标记 · 可空 |
| `status` | varchar(32) | 状态 生效：VALID;失效:INVALID · 可空 |
| `effective_time` | timestamp | 生效时间 |
| `expired_time` | timestamp | 过期时间 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 修改时间 |
| `voucher_no` | varchar(32) | 订单号 · 可空 |
| `order_type` | varchar(32) | 订单类型：COUPON；优惠券：LULU；LuLu商户：TAXI:出租车；UTILITIES_OR_TOP_UP:公众缴费|手机充值 · 可空 |
| `extension` | varchar(225) | 扩展参数 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_created_time`:created_time
- `idx_mid_source`:member_id, source

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

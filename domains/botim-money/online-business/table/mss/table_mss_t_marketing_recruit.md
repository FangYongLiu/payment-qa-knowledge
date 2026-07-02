---
id: tbl_mss_t_marketing_recruit
object_type: Table
name: 营销优惠券待招领记录表 (t_marketing_recruit)
aliases: [t_marketing_recruit, mss.t_marketing_recruit]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mss schema DDL
tags: [online-business, mss]
sensitivity: normal
related_services: []
---

# 营销优惠券待招领记录表 (t_marketing_recruit)

## 用途
物理表 `mss.t_marketing_recruit`,主键 `recruit_id`。营销优惠券待招领记录表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `recruit_id` | bigint | 主键 |
| `contact` | varchar(64) | 联系方式 |
| `request_id` | bigint | 请求ID |
| `request_no` | varchar(64) | 请求编号 |
| `scenes_code` | varchar(64) | 场景码 |
| `biz_type` | varchar(64) | 业务类型（活动子类） |
| `product_code` | varchar(32) | 产品码 · 可空 |
| `pay_Channel` | varchar(32) | 支付渠道 · 可空 |
| `pay_scene` | varchar(32) | 支付场景 · 可空 |
| `trade_amount` | varchar(32) | 交易金额 · 可空 |
| `merchant_id` | varchar(32) | 发券支持的商户号 · 可空 |
| `partner` | varchar(32) | 合作平台 · 可空 |
| `recruit_status` | varchar(64) | 代招领状态 |
| `recruit_amount` | decimal(8, 4) | 代招领金额 · 可空 |
| `effective_time` | timestamp | 生效时间 |
| `exprie_time` | timestamp | 过期时间 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`recruit_id`
- `idx_notify_time`:contact

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_mss_t_coupon_entity
object_type: Table
name: 券实体表 (t_coupon_entity)
aliases: [t_coupon_entity, mss.t_coupon_entity]
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

# 券实体表 (t_coupon_entity)

## 用途
物理表 `mss.t_coupon_entity`,主键 `coupon_entity_id`。券实体表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `coupon_entity_id` | bigint | 主键id |
| `request_no` | varchar(64) | 报名类型 · 可空 |
| `coupon_no` | varchar(64) | 券号 按照一定的算法实现 |
| `coupon_random` | varchar(32) | 随机校验码 |
| `award_item_id` | bigint | 奖品模板id |
| `activity_code` | varchar(64) | 活动id |
| `tool_id` | int | 工具id · 可空 |
| `member_id` | varchar(64) | 会员号 · 可空 |
| `coupon_type` | varchar(32) | 券类型 比例，定额 |
| `coupon_sub_type` | varchar(32) | 优惠券子类型 · 可空 |
| `coupon_attr` | char(4) | 使用类型，m-多张叠加，s-单张 |
| `link_url` | varchar(100) | 跳转地址 · 可空 |
| `award_url` | varchar(255) | 实物奖品url · 可空 |
| `coupon_amount` | decimal(15, 4) | 券额度 定额时必须 · 可空 |
| `coupon_percent` | decimal(8, 4) | 折扣比例 比例时必须 · 可空 |
| `account_no` | varchar(64) | 账户号 券对应出金账户 · 可空 |
| `account_type` | varchar(32) | 账户类型 · 可空 |
| `account_mid` | varchar(64) | 营销商户号 · 可空 |
| `currency` | char(3) | 币种 定额时必须 · 可空 |
| `batch_no` | varchar(64) | 批次号 后台每次发券时产生 · 可空 |
| `version_no` | int | 版本号 · 可空 |
| `use_threshold` | decimal(15, 4) | 使用门槛 -1无门槛 |
| `effective_time` | timestamp | 生效时间 |
| `expire_time` | timestamp | 过期时间 |
| `status` | varchar(16) | 状态 unactived，actived，lock，used |
| `org_coupon_no` | varchar(64) | 券号 按照一定的算法实现=>原券号 · 可空 |
| `is_refunded` | char | 已退标记 · 可空 |
| `discount_amount` | decimal(15, 4) | 抵扣金额 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 更新时间 |
| `upper_limit` | decimal(8, 4) | 折扣上限 · 可空 |
| `coupon_source` | varchar(32) | 来源 · 可空 |

## 主键 / 索引
- 主键:`coupon_entity_id`
- `idx_activity_code`:activity_code
- `idx_coupon_no`:coupon_no
- `idx_create_time`:created_time
- `idx_member_id`:member_id
- `idx_org_coupon_no`:org_coupon_no
- `t_expire_time_index`:expire_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

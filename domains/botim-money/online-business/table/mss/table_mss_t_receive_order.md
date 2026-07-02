---
id: tbl_mss_t_receive_order
object_type: Table
name: 领奖记录 (t_receive_order)
aliases: [t_receive_order, mss.t_receive_order]
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

# 领奖记录 (t_receive_order)

## 用途
物理表 `mss.t_receive_order`,主键 `receive_record_id`。领奖记录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `receive_record_id` | bigint | 主键id |
| `register_id` | bigint | 报名记录 |
| `request_id` | bigint | mq消息ID · 可空 |
| `activity_code` | varchar(64) | 活动id |
| `tool_id` | int | 工具id |
| `tool_type` | varchar(16) | 工具类型 |
| `award_item_id` | int | 奖品id · 可空 |
| `member_id` | varchar(64) | 会员id |
| `relation_mid` | varchar(32) | 关联用户 · 可空 |
| `parent_mid` | varchar(64) | 上级mid · 可空 |
| `reward_level` | int | 奖励等级 · 可空 |
| `org_order_no` | varchar(64) | 原交易订单号 · 可空 |
| `org_merchant_no` | varchar(64) | 原商户订单号 · 可空 |
| `notice_status` | varchar(32) | 通知状态 |
| `status` | varchar(16) | 状态 如success,fail |
| `receive_time` | timestamp | 领奖时间 |
| `amount` | varchar(32) | 金额 · 可空 |
| `currency` | char(3) | 币种 · 可空 |
| `utm_source` | varchar(32) | 来源平台 · 可空 |
| `utm_medium` | varchar(32) | 来源类型 · 可空 |
| `partner_id` | varchar(32) | 平台id · 可空 |
| `coupon_entity_id` | bigint | 券id · 可空 |
| `resp_code` | varchar(32) | 返回码 |
| `error_msg` | varchar(32) | 错误信息 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 更新时间 |
| `discount_amount` | decimal(8, 4) | 折扣金额 · 可空 |
| `beneficiary_type` | varchar(16) | 受益人类型 · 可空 |

## 主键 / 索引
- 主键:`receive_record_id`
- `idx_create_time`:created_time
- `idx_mid`:member_id
- `idx_register_id`:register_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

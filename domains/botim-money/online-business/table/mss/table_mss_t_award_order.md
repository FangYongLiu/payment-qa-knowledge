---
id: tbl_mss_t_award_order
object_type: Table
name: 发奖记录 (t_award_order)
aliases: [t_award_order, mss.t_award_order]
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

# 发奖记录 (t_award_order)

## 用途
物理表 `mss.t_award_order`,主键 `order_no`。发奖记录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `order_no` | bigint | 主键id |
| `voucher_no` | varchar(64) | 凭证号 |
| `org_order_no` | varchar(64) | 原交易订单号 |
| `org_merchant_no` | varchar(64) | 原商户订单号 |
| `receive_record_id` | varchar(32) | 领奖记录id |
| `member_id` | varchar(32) | 会员id |
| `relation_mid` | varchar(32) | 关联用户 · 可空 |
| `reward_amount` | decimal(15, 4) | 发奖额度 |
| `reward_type` | varchar(16) | 奖励类型 |
| `reward_sub_type` | varchar(16) | 奖励子类型 |
| `reward_scenes` | varchar(64) | 奖励场景（对应acitivitysubtype） · 可空 |
| `currency` | char(3) | 币种 |
| `award_item_id` | int | 奖品id |
| `activity_code` | varchar(64) | 活动id |
| `tool_id` | int | 工具id |
| `account_no` | varchar(32) | 付款账号 · 可空 |
| `account_type` | varchar(64) | 账号类型 · 可空 |
| `payer_member_id` | varchar(32) | 奖励发放者 |
| `coupon_entity_id` | varchar(64) | 券id · 可空 |
| `remark` | varchar(512) | 备注 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 更新时间 |
| `device_id` | varchar(64) | 设备id · 可空 |
| `status` | varchar(64) | 状态 · 可空 |
| `extension` | varchar(256) | 扩展字段 · 可空 |
| `relation_merchant_id` | varchar(32) | 商户推广员所属商户id · 可空 |
| `relation_commission` | decimal(12, 4) | 商户佣金 · 可空 |
| `invitee_props` | varchar(500) | 被邀请人信息 · 可空 |
| `inviter_props` | varchar(500) | 邀请人信息 · 可空 |

## 主键 / 索引
- 主键:`order_no`
- `idx_create_time`:created_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

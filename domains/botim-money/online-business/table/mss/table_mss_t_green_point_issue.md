---
id: tbl_mss_t_green_point_issue
object_type: Table
name: 积分发放表 (t_green_point_issue)
aliases: [t_green_point_issue, mss.t_green_point_issue]
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

# 积分发放表 (t_green_point_issue)

## 用途
物理表 `mss.t_green_point_issue`,主键 `id`。积分发放表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `remarks` | varchar(128) | 备注 · 可空 |
| `update_time` | timestamp | 更新时间 |
| `member_id` | varchar(32) | 用户支付端会员号 · 可空 |
| `order_no` | varchar(32) | 积分服务记录订单号 · 可空 |
| `reward_amount` | varchar(32) | 奖励数量 · 可空 |
| `reward_sub_type` | varchar(32) | 奖励子类型 · 可空 |
| `reward_type` | varchar(32) | 奖励类型 · 可空 |
| `scenes` | varchar(32) | 奖励场景来源 · 可空 |
| `source` | varchar(32) | 奖励来源 · 可空 |
| `status` | varchar(32) | 发放状态 · 可空 |
| `interest_id` | varchar(64) | 权益id · 可空 |
| `event_id` | varchar(64) | 活动id · 可空 |
| `source_id` | varchar(64) | 请求号 · 可空 |
| `account_no` | varchar(32) | 扣款账号 · 可空 |
| `from_member_id` | varchar(32) | from_member_id · 可空 |
| `link_id` | varchar(128) | link_id · 可空 |
| `extension` | varchar(255) | 扩展字段 · 可空 |
| `origin_merchant_order_no` | varchar(50) | 原始商户订单号 · 可空 |
| `memo` | varchar(256) | 备注 · 可空 |
| `payer_member_id` | varchar(32) | 付款人会员号 · 可空 |
| `account_type` | varchar(32) | 账户类型 · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_order_no`:order_no (UNIQUE)
- `idx_mid_eventid`:member_id, event_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

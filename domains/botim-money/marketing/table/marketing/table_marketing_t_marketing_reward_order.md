---
id: tbl_marketing_t_marketing_reward_order
object_type: Table
name: 营销服务奖励订单 (t_marketing_reward_order)
aliases: [t_marketing_reward_order, marketing.t_marketing_reward_order]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: marketing schema DDL
tags: [marketing, marketing]
sensitivity: normal
related_services: []
---

# 营销服务奖励订单 (t_marketing_reward_order)

## 用途
物理表 `marketing.t_marketing_reward_order`,主键 `id`。营销服务奖励订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键id · 可空 |
| `order_no` | varchar(32) | 订单编号 · 可空 |
| `member_id` | varchar(32) | 会员id · 可空 |
| `partner_id` | varchar(32) | 会员商户号 · 可空 |
| `payer_account_no` | varchar(32) | 付款会员id · 可空 |
| `reward_type` | varchar(32) | 奖励类型 · 可空 |
| `reward_sub_type` | varchar(32) | 奖励子类型 · 可空 |
| `reward_amount` | decimal(15, 4) | 奖励额度 |
| `source` | varchar(32) | 奖励来源 · 可空 |
| `scenes` | varchar(32) | 奖励场景来源 · 可空 |
| `description` | varchar(1024) | 奖励场景来源 · 可空 |
| `status` | varchar(32) | 订单状态 · 可空 |
| `fail_code` | varchar(128) | 错误码 · 可空 |
| `fail_message` | varchar(512) | 错误描述 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后修改时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`id`
- `idx_created_time`:created_time
- `idx_mid`:member_id
- `idx_order_no`:order_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

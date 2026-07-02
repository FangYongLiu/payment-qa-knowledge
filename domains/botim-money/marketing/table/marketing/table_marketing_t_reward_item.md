---
id: tbl_marketing_t_reward_item
object_type: Table
name: reward_item订单 (t_reward_item)
aliases: [t_reward_item, marketing.t_reward_item]
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

# reward_item订单 (t_reward_item)

## 用途
物理表 `marketing.t_reward_item`,主键 `id`。reward_item订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `scenario_code` | varchar(50) | 场景代码 |
| `parent_type` | varchar(50) | 父订单类型 |
| `parent_id` | bigint | 父订单号 |
| `origin_order_id` | varchar(50) | 原始订单号(冗余) · 可空 |
| `origin_merchant_order_no` | varchar(50) | 原始商户订单号(冗余) · 可空 |
| `origin_order_type` | varchar(50) | 原始订单类型(冗余) · 可空 |
| `device_id` | varchar(32) | 设备ID · 可空 |
| `member_id` | varchar(200) | 会员号 |
| `reward_type` | varchar(50) | 奖励类型 |
| `reward_subtype` | varchar(64) | 奖励子类型 · 可空 |
| `amount` | decimal(15, 4) | 奖励数额 · 可空 |
| `status` | varchar(200) | 状态 |
| `fail_code` | varchar(200) | 错误码 · 可空 |
| `fail_message` | varchar(200) | 错误描述 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`id`
- `i_rwdit_ct`:created_time
- `i_rwdit_lut`:last_updated_time
- `i_rwdit_pt`:parent_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_mss_t_lottery_record
object_type: Table
name: 会员抽奖记录表 (t_lottery_record)
aliases: [t_lottery_record, mss.t_lottery_record]
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

# 会员抽奖记录表 (t_lottery_record)

## 用途
物理表 `mss.t_lottery_record`,主键 `id`。会员抽奖记录表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键ID · 可空 |
| `activity_id` | varchar(64) | 活动ID · 可空 |
| `tool_entity_id` | varchar(64) | 券ID · 可空 |
| `award_id` | bigint | 奖品ID · 可空 |
| `member_id` | varchar(32) | 会员ID · 可空 |
| `status` | varchar(32) | 状态 · 可空 |
| `lottery_time` | timestamp | 抽奖日期 · 可空 |
| `create_time` | timestamp | 创建日期 · 可空 |
| `update_time` | timestamp | 修改日期 · 可空 |
| `notice_flag` | varchar(32) | 通知标识：NEED、CANCEL、ALREADY · 可空 |
| `currency` | varchar(32) | 币种 · 可空 |
| `amount` | decimal(19, 2) | 金额 · 可空 |
| `global_id` | bigint | 订单追踪号 · 可空 |
| `request_no` | varchar(32) | 请求编号 · 可空 |
| `extends` | varchar(256) | 扩展字段 · 可空 |
| `utm_source` | varchar(32) | 领奖事件来源 · 可空 |
| `utm_medium` | varchar(32) | 来源类型 · 可空 |
| `activity_type` | varchar(32) | 活动类型 · 可空 |
| `merchant_ids` | varchar(64) | 活动商户 · 可空 |
| `error_message` | varchar(32) | 响应详细 · 可空 |
| `resp_code` | int | 响应码 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_ct_nf`:create_time, notice_flag
- `idx_memberid`:member_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

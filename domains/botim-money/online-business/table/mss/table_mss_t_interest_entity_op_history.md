---
id: tbl_mss_t_interest_entity_op_history
object_type: Table
name: 权益实体操作记录 (t_interest_entity_op_history)
aliases: [t_interest_entity_op_history, mss.t_interest_entity_op_history]
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

# 权益实体操作记录 (t_interest_entity_op_history)

## 用途
物理表 `mss.t_interest_entity_op_history`,主键 `id`。权益实体操作记录。业务语义细节**待补**(表结构来自 DDL)。

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
| `check_point` | varchar(32) | dataeden接入点（CP1003锁定/CP1004注销） · 可空 |
| `error_message` | varchar(128) | 错误信息 · 可空 |
| `risk_event_id` | varchar(64) | dataeden风险事件id · 可空 |
| `interest_entity_id` | varchar(64) | 权益实体id · 可空 |
| `member_id` | varchar(64) | 用户支付端会员号 · 可空 |
| `ok` | tinyint | 操作是否成功 · 可空 |
| `resp_code` | varchar(20) | 返回码 · 可空 |
| `currency` | varchar(20) | 币种 · 可空 |
| `amount` | decimal(11, 2) | 金额 · 可空 |
| `activity_id` | varchar(64) | 活动id · 可空 |
| `tool_id` | varchar(64) | 工具id · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

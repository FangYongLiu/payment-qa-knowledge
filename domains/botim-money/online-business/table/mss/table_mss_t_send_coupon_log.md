---
id: tbl_mss_t_send_coupon_log
object_type: Table
name: 发放接口记录 (t_send_coupon_log)
aliases: [t_send_coupon_log, mss.t_send_coupon_log]
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

# 发放接口记录 (t_send_coupon_log)

## 用途
物理表 `mss.t_send_coupon_log`,主键 `id`。发放接口记录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |
| `error_message` | varchar(128) | 错误消息 · 可空 |
| `ok` | tinyint | 是否成功 · 可空 |
| `resp_code` | smallint | 返回码 · 可空 |
| `activity_id` | varchar(64) | 活动id · 可空 |
| `activity_id_resp` | varchar(64) | 返回的活动id · 可空 |
| `amount` | decimal(19, 2) | 金额 |
| `currency` | varchar(64) | 金额 · 可空 |
| `customer_id` | varchar(64) | 用户id · 可空 |
| `from_customer_id` | varchar(64) | 发放用户id · 可空 |
| `link_id` | varchar(128) | 链接id · 可空 |
| `tool_entity_id` | varchar(64) | 工具实体id · 可空 |
| `tool_id` | varchar(64) | 工具id · 可空 |
| `tool_id_resp` | varchar(64) | 工具id返回 · 可空 |
| `tool_type` | varchar(64) | 工具类型 · 可空 |
| `tool_value` | varchar(64) | 工具值 · 可空 |

## 主键 / 索引
- 主键:`id`
- `index_customer_activity_id`:customer_id, activity_id
- `index_customer_id`:customer_id
- `index_tool_entity_id`:tool_entity_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_mss_t_marketing_tool
object_type: Table
name: 工具 (t_marketing_tool)
aliases: [t_marketing_tool, mss.t_marketing_tool]
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

# 工具 (t_marketing_tool)

## 用途
物理表 `mss.t_marketing_tool`,主键 `tool_id`。工具。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `tool_id` | int | 主键id · 可空 |
| `tool_type` | varchar(16) | 工具类型 |
| `tool_name` | varchar(64) | 工具名称 |
| `max_amount` | decimal(12, 4) | 最大限额 |
| `max_count` | int | 最大限次 |
| `account_no` | varchar(32) | 出金账号 · 可空 |
| `account_type` | varchar(32) | 出金账号类型 · 可空 |
| `account_mid` | varchar(32) | 出金账号所属会员 · 可空 |
| `use_threshold` | decimal(8, 4) | 使用门槛 -1：无门槛 |
| `effective_time` | int | 奖品使用有效时间(单位分钟) -1：无有效期 |
| `effective_start_time` | timestamp | 奖品有效期起始时间 · 可空 |
| `stock_refresh_type` | varchar(16) | 库存刷新类型 |
| `algorithm_type` | varchar(32) | 抽奖算法类型 · 可空 |
| `remark` | varchar(64) | 使用规则简介 · 可空 |
| `app_url` | varchar(64) | app内部跳转url · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`tool_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

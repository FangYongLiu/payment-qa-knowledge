---
id: tbl_mss_t_tool_award_stock
object_type: Table
name: 奖品库存 (t_tool_award_stock)
aliases: [t_tool_award_stock, mss.t_tool_award_stock]
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

# 奖品库存 (t_tool_award_stock)

## 用途
物理表 `mss.t_tool_award_stock`,主键 `stock_id`。奖品库存。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `stock_id` | bigint | 主键id |
| `tool_id` | varchar(32) | 工具id |
| `award_group_id` | int | 奖品组id |
| `award_item_id` | int | 奖品id |
| `award_stock` | int | 库存 |
| `award_weight` | int | 权重 |
| `effective_time` | timestamp | 库存有效开始时间 |
| `expire_time` | timestamp | 库存过期时间 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`stock_id`
- `idx_tool_group`:tool_id, award_group_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

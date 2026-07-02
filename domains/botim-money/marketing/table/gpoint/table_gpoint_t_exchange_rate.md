---
id: tbl_gpoint_t_exchange_rate
object_type: Table
name: 汇率配置 (t_exchange_rate)
aliases: [t_exchange_rate, gpoint.t_exchange_rate]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: gpoint schema DDL
tags: [marketing, gpoint]
sensitivity: normal
related_services: []
---

# 汇率配置 (t_exchange_rate)

## 用途
物理表 `gpoint.t_exchange_rate`,主键 `currency_code`。汇率配置。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `currency_code` | varchar(10) | 币种 |
| `exchange_amount` | int | 1法币买入数量 |
| `selling_amount` | int | 1法币卖出数量 · 可空 |
| `personal_buying_amount` | int | 个人买入价：1法币买入数量 · 可空 |
| `personal_selling_amount` | int | 个人卖出价：1法币卖出数量 · 可空 |
| `exchange_lower_limit` | int | 汇兑数量下限 |
| `exchange_upper_limit` | int | 汇兑数量上限 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`currency_code`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

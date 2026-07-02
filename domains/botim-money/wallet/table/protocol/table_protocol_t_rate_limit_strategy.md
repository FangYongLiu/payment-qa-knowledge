---
id: tbl_protocol_t_rate_limit_strategy
object_type: Table
name: t_rate_limit_strategy (t_rate_limit_strategy)
aliases: [t_rate_limit_strategy, protocol.t_rate_limit_strategy]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: protocol schema DDL
tags: [wallet, protocol]
sensitivity: normal
related_services: []
---

# t_rate_limit_strategy (t_rate_limit_strategy)

## 用途
物理表 `protocol.t_rate_limit_strategy`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键id · 可空 |
| `show_name` | varchar(64) | 限制策略名称 |
| `strategy_type` | varchar(22) | 策略类型:MERCHANT_ID,PROTOCOL_SUB_TYPE |
| `range_type` | varchar(12) | DAY,MONTH,TOTAL |
| `limit_value` | int | 限制值 · 可空 |
| `strategy_method` | varchar(12) | 策略方式：reject;asyn · 可空 |
| `exclude_node` | varchar(64) | apply:申请协议不限制；direct-sign：直接签约不限制；sign：签约不限制，多个用逗号隔开 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

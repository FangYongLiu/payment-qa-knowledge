---
id: tbl_credit_t_cs_gl_event
object_type: Table
name: 给GL财务系统发交易事件消息记录表，用于记录事件发送情况及失败补偿 (t_cs_gl_event)
aliases: [t_cs_gl_event, credit.t_cs_gl_event]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: credit schema DDL
tags: [lending, credit]
sensitivity: normal
related_services: []
---

# 给GL财务系统发交易事件消息记录表，用于记录事件发送情况及失败补偿 (t_cs_gl_event)

## 用途
物理表 `credit.t_cs_gl_event`,主键 `id`。给GL财务系统发交易事件消息记录表，用于记录事件发送情况及失败补偿。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `order_no` | varchar(64) | 交易事件关联的业务主体no，cashnow的借款订单号 |
| `bus_no` | varchar(64) | 具体交易场景对应事件的唯一标识 |
| `scenario` | varchar(64) | 交易场景 |
| `bus_time` | timestamp | 业务事件发生的时间 · 可空 |
| `detail` | varchar(255) | 事件携带的相关数据参数，json格式 · 可空 |
| `status` | tinyint(5) | 待补 |
| `created_time` | timestamp | 创建日期 · 可空 |
| `last_modified` | timestamp | 修改日期 · 可空 |
| `flag` | smallint | 待补 |

## 主键 / 索引
- 主键:`id`
- `idx_unique_order_no`:order_no, bus_no, scenario (UNIQUE)
- `idx_bus_no`:bus_no
- `idx_bus_time`:bus_time, status
- `idx_created_time`:created_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

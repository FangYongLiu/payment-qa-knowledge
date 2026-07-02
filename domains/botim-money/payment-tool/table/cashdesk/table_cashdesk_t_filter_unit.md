---
id: tbl_cashdesk_t_filter_unit
object_type: Table
name: 渠道过滤单元，同一策略下不同单元为“或”关系 (t_filter_unit)
aliases: [t_filter_unit, cashdesk.t_filter_unit]
domain: payment-tool
status: active
owner: kingo.liang
reviewer: kingo.liang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cashdesk schema DDL
tags: [payment-tool, cashdesk]
sensitivity: normal
related_services: []
---

# 渠道过滤单元，同一策略下不同单元为“或”关系 (t_filter_unit)

## 用途
物理表 `cashdesk.t_filter_unit`,主键 `unit_id`。渠道过滤单元，同一策略下不同单元为“或”关系。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `unit_id` | bigint | 单元id,初始信息手动配置 |
| `filter_id` | bigint | 过滤策略id |
| `pay_mode` | varchar(16) | 支付模式 · 可空 |
| `expression` | varchar(1000) | 执行表达式,velocity表达式 · 可空 |
| `unit_level` | decimal(2) | 优先级 |
| `valid` | char | 是否有效 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 |
| `memo` | varchar(128) | 备注 · 可空 |

## 主键 / 索引
- 主键:`unit_id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

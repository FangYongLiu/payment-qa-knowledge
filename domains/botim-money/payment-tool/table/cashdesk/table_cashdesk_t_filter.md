---
id: tbl_cashdesk_t_filter
object_type: Table
name: 策略表 (t_filter)
aliases: [t_filter, cashdesk.t_filter]
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

# 策略表 (t_filter)

## 用途
物理表 `cashdesk.t_filter`,主键 `filter_id`。策略表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `filter_id` | bigint | 过滤策略id,初始信息手动配置 |
| `filter_name` | varchar(100) | 策略名称 |
| `pay_channel_code` | varchar(16) | 支付渠道代码 |
| `pay_method` | varchar(128) | 支付方式（多项逗号分隔） · 可空 |
| `expression` | varchar(1000) | 执行表达式,velocity表达式 · 可空 |
| `effect_time` | timestamp | 生效时间 |
| `failure_time` | timestamp | 失效时间 |
| `valid` | char | 是否可用，y-是；n-否 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 |
| `memo` | varchar(128) | 备注 · 可空 |

## 主键 / 索引
- 主键:`filter_id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

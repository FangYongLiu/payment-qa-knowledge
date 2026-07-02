---
id: tbl_cashdesk_tm_channel_filter
object_type: Table
name: 渠道过滤策略表 (tm_channel_filter)
aliases: [tm_channel_filter, cashdesk.tm_channel_filter]
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

# 渠道过滤策略表 (tm_channel_filter)

## 用途
物理表 `cashdesk.tm_channel_filter`,主键 `FILTER_ID`。渠道过滤策略表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `FILTER_ID` | decimal | 过滤策略ID,初始信息手动配置 |
| `FILTER_NAME` | varchar(100) | 待补 |
| `PAY_CHANNEL_CODE` | varchar(16) | 支付渠道代码 |
| `EXPRESSION` | varchar(1000) | 执行表达式,Velocity表达式 · 可空 |
| `FILTER_LEVEL` | decimal(2) | 优先级 |
| `EFFECT_TIME` | timestamp | 生效时间 |
| `FAILURE_TIME` | timestamp | 失效时间 |
| `VALID` | char | 是否可用，Y-是；N-否 |
| `IS_BASIC` | char | 是否基础策略，Y-是；N-否 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 修改时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |
| `ANONY_FLAG` | char | 匿名标志 Y-匿名； 默认-非匿名 · 可空 |
| `IS_SHORT_CIRCUIT` | char | 是否短路，Y-是；N-否 · 可空 |

## 主键 / 索引
- 主键:`FILTER_ID`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

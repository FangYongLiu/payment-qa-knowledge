---
id: tbl_credit_t_cs_paylater_auto_repay_config
object_type: Table
name: 定时扣款配置 (t_cs_paylater_auto_repay_config)
aliases: [t_cs_paylater_auto_repay_config, credit.t_cs_paylater_auto_repay_config]
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

# 定时扣款配置 (t_cs_paylater_auto_repay_config)

## 用途
物理表 `credit.t_cs_paylater_auto_repay_config`,主键 `id`。定时扣款配置。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `created_time` | timestamp | 创建时间 · 可空 |
| `last_modified` | timestamp | 修改时间 · 可空 |
| `start` | int(5) | 逾期天数开始时间 · 可空 |
| `end` | int(5) | 逾期天数结束时间 · 可空 |
| `frequency` | int(5) | 执行频率每天次数 · 可空 |
| `time` | varchar(100) | 执行时间 |
| `status` | tinyint(5) | 0无效1有效 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

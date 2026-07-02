---
id: tbl_benefit_t_benefit_metrics
object_type: Table
name: t_benefit_metrics (t_benefit_metrics)
aliases: [t_benefit_metrics, benefit.t_benefit_metrics]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: benefit schema DDL
tags: [marketing, benefit]
sensitivity: normal
related_services: []
---

# t_benefit_metrics (t_benefit_metrics)

## 用途
物理表 `benefit.t_benefit_metrics`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 自增id · 可空 |
| `metric_type` | varchar(50) | 指标类型 |
| `metric_code` | varchar(50) | 指标代码 |
| `metric_val` | decimal(19, 4) | 指标值 · 可空 |
| `memo` | varchar(255) | 备注信息 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_metric_code`:metric_type, metric_code (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

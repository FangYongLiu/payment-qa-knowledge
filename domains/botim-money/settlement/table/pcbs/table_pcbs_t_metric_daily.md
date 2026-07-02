---
id: tbl_pcbs_t_metric_daily
object_type: Table
name: Metric Daily (t_metric_daily)
aliases: [t_metric_daily, pcbs.t_metric_daily]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: pcbs schema DDL
tags: [settlement, pcbs]
sensitivity: normal
related_services: []
---

# Metric Daily (t_metric_daily)

## 用途
物理表 `pcbs.t_metric_daily`,主键 `metric_id`。Metric Daily。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `metric_id` | bigint | Metric ID |
| `metric_date` | date | Metric Date |
| `metric_code` | varchar(50) | Metric Code |
| `metric_sub_code` | varchar(50) | Metric Sub Code · 可空 |
| `count` | int | Count · 可空 |
| `amount` | decimal(19, 4) | Amount · 可空 |
| `create_time` | timestamp | Create time |

## 主键 / 索引
- 主键:`metric_id`
- `idx_create_time`:create_time
- `idx_metric_date_metric_code`:metric_date, metric_code

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

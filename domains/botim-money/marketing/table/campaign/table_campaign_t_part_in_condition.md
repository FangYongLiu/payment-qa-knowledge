---
id: tbl_campaign_t_part_in_condition
object_type: Table
name: t_part_in_condition (t_part_in_condition)
aliases: [t_part_in_condition, campaign.t_part_in_condition]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: campaign schema DDL
tags: [marketing, campaign]
sensitivity: normal
related_services: []
---

# t_part_in_condition (t_part_in_condition)

## 用途
物理表 `campaign.t_part_in_condition`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 |
| `cmpn_id` | bigint | 活动id · 可空 |
| `op_type` | varchar(15) | 操作类型 · 可空 |
| `data_type` | varchar(15) | 数据类型 RULE（dataEden）  DEFAULT · 可空 |
| `data_key` | varchar(50) | 参数名 · 可空 |
| `compare_val` | varchar(255) | 对比值 · 可空 |
| `status` | tinyint | 是否可用 0 不可用 1可用 · 可空 |
| `c_type` | varchar(10) | 条件类型 INNER内部使用 CONFIG页面配置使用 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_cmpn_id`:cmpn_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

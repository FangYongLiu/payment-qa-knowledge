---
id: tbl_collection_t_ia_control_feature
object_type: Table
name: 反欺诈特征表 (t_ia_control_feature)
aliases: [t_ia_control_feature, collection.t_ia_control_feature]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: collection schema DDL
tags: [risk, collection]
sensitivity: normal
related_services: []
---

# 反欺诈特征表 (t_ia_control_feature)

## 用途
物理表 `collection.t_ia_control_feature`,主键 `id`。反欺诈特征表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主健 · 可空 |
| `create_by` | varchar(64) | 创建者 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |
| `update_by` | varchar(64) | 更新人员 · 可空 |
| `uid` | varchar(64) | 本数据id |
| `order_no` | varchar(64) | 订单号 |
| `des_cn` | varchar(255) | 中文描述 · 可空 |
| `des_en` | varchar(255) | 英文描述 · 可空 |
| `threshold` | varchar(30) | 阙值 · 可空 |
| `value_type` | varchar(5) | 类型 1数字 2布尔 · 可空 |
| `feature_value` | varchar(20) | 特征值 · 可空 |
| `feature_code` | varchar(20) | 特征代码 · 可空 |
| `feature_id` | varchar(20) | 特征id · 可空 |
| `code` | varchar(20) | 特征代码 · 可空 |
| `code_priority` | varchar(10) | 特征优先级 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_order_no`:order_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

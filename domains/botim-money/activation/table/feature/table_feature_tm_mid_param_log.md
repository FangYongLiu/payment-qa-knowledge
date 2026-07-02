---
id: tbl_feature_tm_mid_param_log
object_type: Table
name: 会员参数日志表 (tm_mid_param_log)
aliases: [tm_mid_param_log, feature.tm_mid_param_log]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: feature schema DDL
tags: [activation, feature]
sensitivity: normal
related_services: []
---

# 会员参数日志表 (tm_mid_param_log)

## 用途
物理表 `feature.tm_mid_param_log`,主键 `mid_param_log_id`。会员参数日志表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `mid_param_log_id` | bigint | 主键ID |
| `mid_param_id` | bigint | 会员参数ID · 可空 |
| `member_id` | varchar(32) | 会员ID · 可空 |
| `param_name` | varchar(32) | 参数名称 · 可空 |
| `param_type` | varchar(32) | 参数类型 · 可空 |
| `param_sub_type` | varchar(32) | 参数子类 · 可空 |
| `param_value` | varchar(32) | 参数值 · 可空 |
| `param_status` | varchar(32) | 参数状态 · 可空 |
| `created_time` | timestamp | 创建时间 · 可空 |
| `updated_time` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`mid_param_log_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

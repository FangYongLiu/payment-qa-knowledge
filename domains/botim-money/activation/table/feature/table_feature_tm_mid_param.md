---
id: tbl_feature_tm_mid_param
object_type: Table
name: 会员参数表 (tm_mid_param)
aliases: [tm_mid_param, feature.tm_mid_param]
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

# 会员参数表 (tm_mid_param)

## 用途
物理表 `feature.tm_mid_param`,主键 `mid_param_id`。会员参数表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `mid_param_id` | bigint | 主键ID |
| `member_id` | varchar(32) | 会员ID |
| `param_name` | varchar(32) | 参数名称 |
| `param_type` | varchar(32) | 参数类型 |
| `param_sub_type` | varchar(32) | 参数子类 |
| `param_value` | varchar(32) | 参数值 |
| `param_status` | varchar(32) | 参数状态 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`mid_param_id`
- `i_member_id`:member_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_feature_tm_feature_apply
object_type: Table
name: 会员功能申请表 (tm_feature_apply)
aliases: [tm_feature_apply, feature.tm_feature_apply]
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

# 会员功能申请表 (tm_feature_apply)

## 用途
物理表 `feature.tm_feature_apply`,主键 `apply_id`。会员功能申请表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `apply_id` | bigint | 主键ID |
| `member_id` | varchar(32) | 会员ID |
| `feature_name` | varchar(32) | 功能名称 |
| `partner_id` | varchar(32) | 平台ID |
| `apply_type` | varchar(32) | 申请类型 |
| `apply_step` | varchar(32) | 当前步骤 |
| `apply_status` | varchar(32) | 流程状态 |
| `created_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |
| `memo` | varchar(32) | 备注信息 · 可空 |

## 主键 / 索引
- 主键:`apply_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

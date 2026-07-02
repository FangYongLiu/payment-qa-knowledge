---
id: tbl_mss_t_marketing_common_setting
object_type: Table
name: 营销系统通用设置 (t_marketing_common_setting)
aliases: [t_marketing_common_setting, mss.t_marketing_common_setting]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mss schema DDL
tags: [online-business, mss]
sensitivity: normal
related_services: []
---

# 营销系统通用设置 (t_marketing_common_setting)

## 用途
物理表 `mss.t_marketing_common_setting`,主键 `id`。营销系统通用设置。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键ID · 可空 |
| `param_type` | varchar(32) | 参数类型 |
| `param_key` | varchar(64) | 参数key |
| `param_value` | varchar(255) | 参数value |
| `status` | varchar(16) | 状态 |
| `created_time` | timestamp | 创建时间 · 可空 |
| `updated_time` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `UK_COMMON_SETTING`:param_type, param_key (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

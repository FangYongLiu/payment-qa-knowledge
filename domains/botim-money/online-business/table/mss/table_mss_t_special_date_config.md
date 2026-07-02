---
id: tbl_mss_t_special_date_config
object_type: Table
name: 特殊日期配置 (t_special_date_config)
aliases: [t_special_date_config, mss.t_special_date_config]
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

# 特殊日期配置 (t_special_date_config)

## 用途
物理表 `mss.t_special_date_config`,主键 `id`。特殊日期配置。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键ID · 可空 |
| `activity_code` | varchar(64) | 关联活动 |
| `day_category` | varchar(32) | 日期类型 |
| `day_content` | varchar(200) | 日期配置内容 |
| `day_status` | char(2) | 日期配置状态 |
| `created_time` | timestamp | 创建时间 · 可空 |
| `updated_time` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

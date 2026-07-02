---
id: tbl_credit_t_cs_gray_config
object_type: Table
name: Gray configuration table (t_cs_gray_config)
aliases: [t_cs_gray_config, credit.t_cs_gray_config]
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

# Gray configuration table (t_cs_gray_config)

## 用途
物理表 `credit.t_cs_gray_config`,主键 `id`。Gray configuration table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key ID · 可空 |
| `gray_scene` | varchar(32) | Gray scenario, e.g., ui2 |
| `gray_config` | varchar(1024) | Gray configuration JSON, including channel rules · 可空 |
| `whitelist` | varchar(1024) | whitelist, JSON format: {"deviceId":"forceTag"} · 可空 |
| `default_gray_tag` | varchar(25) | Default gray tag, returned when users do not enter the gray phase · 可空 |
| `gray_status` | tinyint | Gray status: 0-inactive, 1-active, 2-short-circuited · 可空 |
| `version` | int | cas version |
| `create_time` | timestamp | Creation time · 可空 |
| `update_time` | timestamp | Update time · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_gray_scene`:gray_scene (UNIQUE)
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

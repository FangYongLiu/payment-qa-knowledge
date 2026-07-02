---
id: tbl_csc_t_compare_define
object_type: Table
name: 对账定义 (t_compare_define)
aliases: [t_compare_define, csc.t_compare_define]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: csc schema DDL
tags: [merchant-management, csc]
sensitivity: normal
related_services: []
---

# 对账定义 (t_compare_define)

## 用途
物理表 `csc.t_compare_define`,主键 `define_id`。对账定义。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `define_id` | bigint | 定义ID · 可空 |
| `define_name` | varchar(128) | 定义名称 |
| `src_datasource_code` | varchar(32) | 源数据源代码 |
| `src_sql_template` | text | 源数据查询模版 |
| `src_split_minutes` | int | 源数据切分时长 |
| `src_relate_field` | varchar(32) | 源数据关联字段 |
| `target_datasource_code` | varchar(32) | 目标数据源代码 |
| `target_sql_template` | text | 目标数据查询模版 |
| `target_relate_field` | varchar(32) | 目标数据关联字段 |
| `target_sharding_expression` | varchar(128) | 目标数据分片表达式 · 可空 |
| `check_expression` | varchar(1000) | 校验表达式 |
| `compensate_expression` | varchar(1000) | 补单表达式 · 可空 |
| `compensate_config` | varchar(128) | 补单配置 · 可空 |
| `enable_flag` | char | 启用标志：Y=启用，N=停用 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`define_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

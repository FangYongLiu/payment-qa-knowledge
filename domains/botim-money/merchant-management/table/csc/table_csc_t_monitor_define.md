---
id: tbl_csc_t_monitor_define
object_type: Table
name: 监控定义 (t_monitor_define)
aliases: [t_monitor_define, csc.t_monitor_define]
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

# 监控定义 (t_monitor_define)

## 用途
物理表 `csc.t_monitor_define`,主键 `define_id`。监控定义。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `define_id` | bigint | 定义ID · 可空 |
| `application_name` | varchar(128) | 应用名称 |
| `define_name` | varchar(128) | 定义名称 |
| `datasource_type` | varchar(10) | 数据源类型：MYSQL，ES |
| `datasource_code` | varchar(128) | 数据源代码 |
| `query_template` | text | 查询模版 |
| `monitor_type` | char | 监控类型：R=报表，A=报警 |
| `priority` | char | 优先级：H=高，M=中，L=低 |
| `split_strategy` | varchar(10) | 切分策略：NO=不切分，UNION=拼接，SUM=汇总 |
| `split_minutes` | int | 数据切分时长 · 可空 |
| `key_field` | varchar(128) | 关键字段 · 可空 |
| `notify_expression` | varchar(1000) | 通知表达式 · 可空 |
| `enable_flag` | char | 启用标识：Y=启用，N=停用 |
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

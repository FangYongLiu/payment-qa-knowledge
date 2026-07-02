---
id: tbl_basismcht_tb_uq_define
object_type: Table
name: 联合查询定义 (tb_uq_define)
aliases: [tb_uq_define, basismcht.tb_uq_define]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: basismcht schema DDL
tags: [merchant-management, basismcht]
sensitivity: normal
related_services: []
---

# 联合查询定义 (tb_uq_define)

## 用途
物理表 `basismcht.tb_uq_define`,主键 `define_id`。联合查询定义。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `define_id` | bigint(10) | 定义ID · 可空 |
| `name` | varchar(64) | 名称 |
| `source_id` | bigint(10) | 数据源ID |
| `sql_content` | text | SQL语句 |
| `priority_level` | bigint(3) | 优先级 |
| `sql_usage` | varchar(8) | 用途 · 可空 |
| `sql_explain` | varchar(128) | 说明 · 可空 |
| `status` | varchar(1) | 状态。U：不可用;N：正常 |
| `memo` | varchar(128) | 备注 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 最后修改时间 |

## 主键 / 索引
- 主键:`define_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

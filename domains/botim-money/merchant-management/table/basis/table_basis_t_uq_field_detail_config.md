---
id: tbl_basis_t_uq_field_detail_config
object_type: Table
name: 联合查询字段明细配置 (t_uq_field_detail_config)
aliases: [t_uq_field_detail_config, basis.t_uq_field_detail_config]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: basis schema DDL
tags: [merchant-management, basis]
sensitivity: normal
related_services: []
---

# 联合查询字段明细配置 (t_uq_field_detail_config)

## 用途
物理表 `basis.t_uq_field_detail_config`,主键 `config_id`。联合查询字段明细配置。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `config_id` | bigint | 配置ID · 可空 |
| `define_id` | bigint | 定义ID |
| `detail_type` | varchar(64) | 详情类型 Form:弹出框 url:超链接 |
| `field_name` | varchar(32) | 字段名称 |
| `type_value` | varchar(255) | 字段类型值 · 可空 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `memo` | varchar(512) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`config_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

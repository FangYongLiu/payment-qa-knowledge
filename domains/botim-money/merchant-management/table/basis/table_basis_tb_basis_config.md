---
id: tbl_basis_tb_basis_config
object_type: Table
name: basis综合配置表 (tb_basis_config)
aliases: [tb_basis_config, basis.tb_basis_config]
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

# basis综合配置表 (tb_basis_config)

## 用途
物理表 `basis.tb_basis_config`,主键 `config_id`。basis综合配置表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `config_id` | bigint | 配置ID · 可空 |
| `config_code` | varchar(128) | 配置名称 |
| `config_value` | varchar(1000) | 配置值 · 可空 |
| `memo` | varchar(128) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`config_id`
- `uk_config_code`:config_code (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

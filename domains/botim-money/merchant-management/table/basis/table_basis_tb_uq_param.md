---
id: tbl_basis_tb_uq_param
object_type: Table
name: 联合查询参数 (tb_uq_param)
aliases: [tb_uq_param, basis.tb_uq_param]
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

# 联合查询参数 (tb_uq_param)

## 用途
物理表 `basis.tb_uq_param`,主键 `param_id`。联合查询参数。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `param_id` | bigint(10) | 主键id · 可空 |
| `define_id` | bigint(10) | 定义ID |
| `field_name` | varchar(32) | 字段名称 |
| `order_type` | varchar(32) | 订单类型 |
| `sql_suffix` | varchar(255) | sql后缀 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `memo` | varchar(128) | 备注 · 可空 |

## 主键 / 索引
- 主键:`param_id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

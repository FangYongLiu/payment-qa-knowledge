---
id: tbl_bill_t_view_field_config
object_type: Table
name: 视图字段配置 (t_view_field_config)
aliases: [t_view_field_config, bill.t_view_field_config]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: bill schema DDL
tags: [payment-core, bill]
sensitivity: normal
related_services: []
---

# 视图字段配置 (t_view_field_config)

## 用途
物理表 `bill.t_view_field_config`,主键 `field_id`。视图字段配置。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `field_id` | bigint | 配置ID · 可空 |
| `view_id` | bigint | 视图ID |
| `show_flag` | char | 是否显示：Y=是，N=否 |
| `priority` | int | 优先级 · 可空 |
| `field_code` | varchar(64) | 字段代码 |
| `name_expression` | varchar(2000) | 名称表达式 |
| `value_expression` | varchar(2000) | 值表达式 |
| `value_type` | varchar(64) | Date/ToTok/String/Money/User · 可空 |
| `style` | varchar(32) | primary|warning|ghost · 可空 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `enable_flag` | char | 启用标识：Y=启用，N=停用 |
| `memo` | varchar(255) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`field_id`
- `uk_viewid_fieldcode`:view_id, field_code (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

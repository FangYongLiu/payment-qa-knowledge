---
id: tbl_feebill_t_view_field_config
object_type: Table
name: View Field Config (t_view_field_config)
aliases: [t_view_field_config, feebill.t_view_field_config]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: feebill schema DDL
tags: [payment-core, feebill]
sensitivity: normal
related_services: []
---

# View Field Config (t_view_field_config)

## 用途
物理表 `feebill.t_view_field_config`,主键 `field_id`。View Field Config。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `field_id` | int | Field Id · 可空 |
| `view_id` | int | View Id |
| `show_flag` | char | Show Flag |
| `priority` | int | Priority |
| `field_code` | varchar(32) | Field Code |
| `name_expression` | varchar(512) | Name Expression |
| `value_expression` | varchar(512) | Value Expression |
| `enable_flag` | char | Enable flag: Y=Yes，N=No |
| `extension` | varchar(255) | Extension · 可空 |
| `memo` | varchar(100) | Memo · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`field_id`
- `view_id`:view_id, field_code (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_feebill_t_view_config
object_type: Table
name: View Config (t_view_config)
aliases: [t_view_config, feebill.t_view_config]
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

# View Config (t_view_config)

## 用途
物理表 `feebill.t_view_config`,主键 `view_id`。View Config。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `view_id` | int | View Id · 可空 |
| `view_code` | varchar(32) | View Code |
| `title_expression` | varchar(128) | Title Expression · 可空 |
| `access_type` | char | Access Type |
| `enable_flag` | char | Enable flag: Y=Yes，N=No |
| `data_filter` | varchar(1024) | Data Filter · 可空 |
| `extension` | varchar(512) | Extension · 可空 |
| `memo` | varchar(100) | Memo · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`view_id`
- `uk_view_code`:view_code (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

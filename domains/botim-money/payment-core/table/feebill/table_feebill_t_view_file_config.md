---
id: tbl_feebill_t_view_file_config
object_type: Table
name: View File Config (t_view_file_config)
aliases: [t_view_file_config, feebill.t_view_file_config]
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

# View File Config (t_view_file_config)

## 用途
物理表 `feebill.t_view_file_config`,主键 `file_config_id`。View File Config。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `file_config_id` | int | File Config Id · 可空 |
| `view_code` | varchar(32) | View Code |
| `period_type` | varchar(32) | Period Type |
| `file_type` | varchar(10) | File Type: default=PDF |
| `valid_minutes` | int | Valid Minutes |
| `refresh_minutes` | int | Refresh Minutes |
| `template_file_path` | varchar(64) | Template File Path |
| `enable_flag` | char | Enable flag: Y=Yes，N=No |
| `extension` | varchar(2048) | Extension · 可空 |
| `memo` | varchar(100) | Memo · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`file_config_id`
- `view_code`:view_code, period_type, file_type (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

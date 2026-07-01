---
id: tbl_acs_t_translate_config
object_type: Table
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (acs schema) 2026-06-25
tags:
- acs
- acs
- t_translate_config
subdomain: acs
module: null
sensitivity: normal
name: 名词翻译配置表(t_translate_config)
aliases:
- t_translate_config
related_services:
- svc_acs
related_scenarios: []
---
# 名词翻译配置表(t_translate_config)

## 用途
名词翻译配置表。属 acs 库,由 [[svc_acs]] 读写。

## 关联关系
- **所属服务**:[[svc_acs]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `config_id` | bigint | PK / AUTO_INC |  |
| `config_code` | varchar(64) | NOT NULL | 编码 |
| `config_key` | varchar(32) | NOT NULL | 占位符 |
| `config_value` | varchar(128) | NOT NULL | 编码+占位符对应的值 |
| `memo` | varchar(200) |  | 备注 |
| `gmt_create` | timestamp | NOT NULL | 创建时间 |
| `gmt_modified` | timestamp | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`config_id`)
- 唯一约束:
  - `uk_code_key` 唯一 (config_code, config_key)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

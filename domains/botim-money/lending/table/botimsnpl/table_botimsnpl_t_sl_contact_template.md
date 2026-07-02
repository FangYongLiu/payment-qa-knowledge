---
id: tbl_botimsnpl_t_sl_contact_template
object_type: Table
name: 合同模板表 (t_sl_contact_template)
aliases: [t_sl_contact_template, botimsnpl.t_sl_contact_template]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: botimsnpl schema DDL
tags: [lending, botimsnpl]
sensitivity: normal
related_services: []
---

# 合同模板表 (t_sl_contact_template)

## 用途
物理表 `botimsnpl.t_sl_contact_template`,主键 `id`。合同模板表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 自增id · 可空 |
| `name` | varchar(128) | 模板名称 |
| `version` | int(64) | 版本 |
| `html_content` | text | 模板html内容 |
| `create_time` | timestamp | 入库时间 |
| `file_name` | varchar(128) | 给用户发送消息时的文件名，其中含有占位符 · 可空 |
| `file_size` | int | 此模版生成的pdf文件大小 · 可空 |

## 主键 / 索引
- 主键:`id`
- `name_version_idx`:name, version (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

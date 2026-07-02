---
id: tbl_reconciliation_t_file_parse_script
object_type: Table
name: 渠道解析脚本 (t_file_parse_script)
aliases: [t_file_parse_script, reconciliation.t_file_parse_script]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: reconciliation schema DDL
tags: [settlement, reconciliation]
sensitivity: normal
related_services: []
---

# 渠道解析脚本 (t_file_parse_script)

## 用途
物理表 `reconciliation.t_file_parse_script`,主键 `script_id`。渠道解析脚本。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `script_id` | int | 待补 · 可空 |
| `name` | varchar(64) | 脚本名称 · 可空 |
| `script_type` | varchar(8) | 脚本类型 资金清算脚本、手续费解析脚本 · 可空 |
| `fund_channel_code` | varchar(32) | 渠道编号 · 可空 |
| `biz_type` | varchar(8) | 业务类型 · 可空 |
| `file_type` | varchar(8) | 文件类型 txt,csv,xls · 可空 |
| `script_content` | longtext | 脚本内容 · 可空 |
| `gmt_create` | timestamp | 创建日期 |
| `gmt_modified` | timestamp | 更新日期 |

## 主键 / 索引
- 主键:`script_id`
- `uk_channel_bizType_scriptType`:fund_channel_code, biz_type, script_type (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

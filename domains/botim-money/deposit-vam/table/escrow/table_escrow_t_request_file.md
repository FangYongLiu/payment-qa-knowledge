---
id: tbl_escrow_t_request_file
object_type: Table
name: 请求文件信息表 (t_request_file)
aliases: [t_request_file, escrow.t_request_file]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: escrow schema DDL
tags: [deposit-vam, escrow]
sensitivity: normal
related_services: []
---

# 请求文件信息表 (t_request_file)

## 用途
物理表 `escrow.t_request_file`,主键 `file_id`。请求文件信息表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `file_id` | bigint(19) | id |
| `file_name` | varchar(255) | 文件名 · 可空 |
| `file_type` | varchar(4) | 文件类型 · 可空 |
| `file_date` | date | 文件日期 · 可空 |
| `STATUS` | varchar(4) | 状态 · 可空 |
| `file_path` | varchar(255) | 文件路径 · 可空 |
| `memo` | varchar(255) | memo · 可空 |
| `gmt_create` | timestamp | 创建日期 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |
| `resp_file_tag` | varchar(255) | 响应文件路径 · 可空 |

## 主键 / 索引
- 主键:`file_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

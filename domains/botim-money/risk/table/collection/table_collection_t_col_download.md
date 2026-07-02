---
id: tbl_collection_t_col_download
object_type: Table
name: 下载文件 (t_col_download)
aliases: [t_col_download, collection.t_col_download]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: collection schema DDL
tags: [risk, collection]
sensitivity: normal
related_services: []
---

# 下载文件 (t_col_download)

## 用途
物理表 `collection.t_col_download`,主键 `id`。下载文件。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(11) | 待补 · 可空 |
| `create_by` | varchar(100) | 创建者 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |
| `update_by` | varchar(100) | 更新人员 · 可空 |
| `uid` | varchar(50) | id · 可空 |
| `create_uid` | varchar(50) | 申请人 · 可空 |
| `param` | varchar(255) | 申请参数 · 可空 |
| `date` | varchar(10) | 查询日期参数 · 可空 |
| `status` | smallint(5) | 状态 0 1成功 -1 失败 · 可空 |
| `type` | smallint(5) | 1质检报告 · 可空 |
| `name` | varchar(50) | 展示名称 · 可空 |
| `start_time` | timestamp | 开始处理时间 · 可空 |
| `end_time` | timestamp | 结束处理时间 · 可空 |
| `download_count` | smallint(5) | 下载次数 · 可空 |
| `file_tag` | varchar(100) | 文件存储名 · 可空 |
| `file_size` | int(10) | 文件大小 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

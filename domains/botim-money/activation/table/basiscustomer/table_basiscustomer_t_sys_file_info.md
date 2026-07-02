---
id: tbl_basiscustomer_t_sys_file_info
object_type: Table
name: 文件信息表 (t_sys_file_info)
aliases: [t_sys_file_info, basiscustomer.t_sys_file_info]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: basiscustomer schema DDL
tags: [activation, basiscustomer]
sensitivity: normal
related_services: []
---

# 文件信息表 (t_sys_file_info)

## 用途
物理表 `basiscustomer.t_sys_file_info`,主键 `file_id`。文件信息表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `file_id` | bigint | 主键id · 可空 |
| `file_data` | varchar(128) | base64编码的文件 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 修改时间 · 可空 |
| `create_user` | bigint | 创建用户 · 可空 |
| `update_user` | bigint | 修改用户 · 可空 |

## 主键 / 索引
- 主键:`file_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

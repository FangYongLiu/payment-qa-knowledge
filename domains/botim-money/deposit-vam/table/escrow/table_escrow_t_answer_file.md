---
id: tbl_escrow_t_answer_file
object_type: Table
name: 银行回复文件表 (t_answer_file)
aliases: [t_answer_file, escrow.t_answer_file]
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

# 银行回复文件表 (t_answer_file)

## 用途
物理表 `escrow.t_answer_file`,主键 `id`。银行回复文件表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(19) | id |
| `file_name` | varchar(255) | 文件名称 |
| `file_tag` | varchar(255) | 文件tag · 可空 |
| `bank_code` | varchar(64) | 银行卡编号，用于区分银行 |
| `answer_time` | timestamp | 回复时间 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modify` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_rnpl_t_contract_file
object_type: Table
name: Contract File Table (t_contract_file)
aliases: [t_contract_file, rnpl.t_contract_file]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: rnpl schema DDL
tags: [lending, rnpl]
sensitivity: normal
related_services: []
---

# Contract File Table (t_contract_file)

## 用途
物理表 `rnpl.t_contract_file`,主键 `id`。Contract File Table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | Self-incrementing ID · 可空 |
| `contract_id` | int | contract id |
| `file_type` | varchar(32) | file type |
| `file_tag` | varchar(128) | photo tag number of contract · 可空 |
| `batch_no` | varchar(128) | batch number of contract photos |
| `status` | smallint(4) | contract manual review of the state, 0: pending review; 1: review through; 2: review rejected |
| `create_time` | timestamp | create time |
| `update_time` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- `uk_ft`:file_tag (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_sme_t_notify_record
object_type: Table
name: Notification record (t_notify_record)
aliases: [t_notify_record, sme.t_notify_record]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: sme schema DDL
tags: [lending, sme]
sensitivity: normal
related_services: []
---

# Notification record (t_notify_record)

## 用途
物理表 `sme.t_notify_record`,主键 `id`。Notification record。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(11) | 待补 · 可空 |
| `notify_code` | char(4) | 待补 |
| `bussiness_id` | varchar(64) | business id |
| `third_party_name` | varchar(20) | Currently, the only third party to which the service belongs is yeahka |
| `status` | smallint | 待补 |
| `yeahka_notify_content` | text | Notify yeahka of the contents · 可空 |
| `fail_num` | tinyint(2) | Number of notification failures |
| `retry_limit` | tinyint(2) | Maximum number of retries allowed |
| `last_notify_time` | timestamp | The latest notification to yeahka · 可空 |
| `create_time` | timestamp | Creation time |
| `update_time` | timestamp | Modification time |

## 主键 / 索引
- 主键:`id`
- `idx_bussiness_id`:bussiness_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

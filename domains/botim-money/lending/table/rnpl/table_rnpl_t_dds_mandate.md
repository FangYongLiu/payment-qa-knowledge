---
id: tbl_rnpl_t_dds_mandate
object_type: Table
name: DDS Mandate Information (t_dds_mandate)
aliases: [t_dds_mandate, rnpl.t_dds_mandate]
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

# DDS Mandate Information (t_dds_mandate)

## 用途
物理表 `rnpl.t_dds_mandate`,主键 `id`。DDS Mandate Information。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | unique id · 可空 |
| `contract_id` | bigint | rent contract id · 可空 |
| `dds_ref_no` | varchar(127) | mandate id by dds · 可空 |
| `dds_mandate_status` | varchar(31) | mandate status · 可空 |
| `mandate_cancelation_status` | varchar(31) | mandate cancel status, null if cancelation request is not initiated · 可空 |
| `create_time` | timestamp | entry create time |
| `update_time` | timestamp | last update time |
| `callback_recieve_time` | timestamp | last update by webhook callback · 可空 |
| `is_in_use` | tinyint(1) | is the mandate currently being used to collect bill · 可空 |
| `is_next_candidate` | tinyint(1) | is the mandate created to replace the current mandate · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_contract_id`:contract_id
- `idx_dds_ref_no`:dds_ref_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

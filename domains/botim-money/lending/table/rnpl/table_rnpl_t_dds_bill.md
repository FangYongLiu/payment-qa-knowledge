---
id: tbl_rnpl_t_dds_bill
object_type: Table
name: DDS Bill mapping (t_dds_bill)
aliases: [t_dds_bill, rnpl.t_dds_bill]
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

# DDS Bill mapping (t_dds_bill)

## 用途
物理表 `rnpl.t_dds_bill`,主键 `id`。DDS Bill mapping。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | unique id · 可空 |
| `bill_id` | bigint | rnpl bill id · 可空 |
| `adg_bill_id` | bigint | adg bill id · 可空 |
| `contract_id` | bigint | rent contract id · 可空 |
| `dds_ref_no` | varchar(127) | mandate id by dds · 可空 |
| `adg_bill_status` | varchar(31) | adg bill status · 可空 |
| `create_time` | timestamp | entry create time |
| `update_time` | timestamp | last update time |
| `callback_receive_time` | timestamp | last update by webhook callback · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_adg_bill_id`:adg_bill_id
- `idx_bill_id`:bill_id
- `idx_contract_id`:contract_id
- `idx_dds_ref_no`:dds_ref_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

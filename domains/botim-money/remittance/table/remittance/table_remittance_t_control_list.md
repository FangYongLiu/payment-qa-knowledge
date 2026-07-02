---
id: tbl_remittance_t_control_list
object_type: Table
name: control list (t_control_list)
aliases: [t_control_list, remittance.t_control_list]
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: remittance schema DDL
tags: [remittance, remittance]
sensitivity: normal
related_services: []
---

# control list (t_control_list)

## 用途
物理表 `remittance.t_control_list`,主键 `id`。control list。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | Primary key |
| `list_name` | varchar(50) | Control list |
| `identifier` | varchar(50) | Identifier value (member_id/phone/id_card) |
| `identifier_type` | varchar(20) | Identifier type: MEMBER_ID, PHONE, 3-EID |
| `status` | tinyint | Status: 0-Disabled, 1-Enabled |
| `source` | varchar(30) | Source:SYSTEM,IMPORT |
| `remark` | varchar(100) | Remark · 可空 |
| `created_time` | timestamp | Created time |
| `updated_time` | timestamp | Updated time |

## 主键 / 索引
- 主键:`id`
- `uk_identifier_type`:list_name, identifier, identifier_type (UNIQUE)
- `idx_created_time`:created_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

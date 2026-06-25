---
id: tbl_remittance_t_i18n
object_type: Table
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (remittance schema) 2026-06-25
tags:
- remittance
- remittance
- t_i18n
subdomain: remittance
module: null
sensitivity: normal
name: Internationalization translation table(t_i18n)
aliases:
- t_i18n
related_services:
- svc_remittance
related_scenarios: []
---
# Internationalization translation table(t_i18n)

## 用途
Internationalization translation table。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | Primary key ID |
| `i18n_key` | varchar(128) | NOT NULL | Translation key |
| `lang_type` | char(3) | NOT NULL | Language type |
| `org_value` | varchar(520) |  | original content |
| `i18n_value` | varchar(520) |  | Translation content |
| `trs_type` | varchar(10) | NOT NULL | Translation source (e.g. AI, MANUAL) |
| `create_time` | timestamp | NOT NULL | Creation time |
| `update_time` | timestamp | NOT NULL | Update time |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_key_lang` 唯一 (i18n_key, lang_type)
- 索引:
  - `idx_lang_type` (lang_type)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

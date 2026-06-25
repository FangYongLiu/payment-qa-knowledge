---
id: tbl_acs_t_unity_code_mapping
object_type: Table
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (acs schema) 2026-06-25
tags:
- acs
- acs
- t_unity_code_mapping
subdomain: acs
module: null
sensitivity: normal
name: 统一码映射配置表(t_unity_code_mapping)
aliases:
- t_unity_code_mapping
related_services:
- svc_acs
related_scenarios: []
---
# 统一码映射配置表(t_unity_code_mapping)

## 用途
统一码映射配置表。属 acs 库,由 [[svc_acs]] 读写。

## 关联关系
- **所属服务**:[[svc_acs]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | 主键 |
| `pattern` | varchar(100) | NOT NULL | 统一结果码 |
| `pattern_type` | varchar(10) | NOT NULL | 模式;full - 全匹配，prefix - 前缀匹配 |
| `mapping_code` | varchar(100) | NOT NULL | 映射码 |
| `code_type` | varchar(30) |  | code 类型(USER_REASON / NONUSER_REASON) |
| `remarks` | varchar(255) |  | 备注 |
| `gmt_created` | timestamp | NOT NULL | 创建时间 |
| `gmt_updated` | timestamp | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_pattern_ptype` 唯一 (pattern, pattern_type)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

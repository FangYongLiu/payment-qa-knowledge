---
id: tbl_remittance_t_bank_code
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
- t_bank_code
subdomain: remittance
module: null
sensitivity: normal
name: bank code table for channel(t_bank_code)
aliases:
- t_bank_code
related_services:
- svc_remittance
related_scenarios: []
---
# bank code table for channel(t_bank_code)

## 用途
bank code table for channel。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC |  |
| `r_bank_code` | varchar(10) |  | bank code from bank info |
| `code_value` | varchar(10) |  | bank code |
| `ca_or_sa_length` | int |  | length of CA or SA |
| `channel_code` | varchar(32) |  |  |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_bdo_bank_code_length` 唯一 (r_bank_code, ca_or_sa_length)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

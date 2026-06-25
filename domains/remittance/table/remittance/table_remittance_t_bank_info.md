---
id: tbl_remittance_t_bank_info
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
- t_bank_info
subdomain: remittance
module: null
sensitivity: normal
name: 银行信息(t_bank_info)
aliases:
- t_bank_info
related_services:
- svc_remittance
related_scenarios: []
---
# 银行信息(t_bank_info)

## 用途
银行信息。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | 主键 |
| `inst_code` | varchar(7) | NOT NULL | 机构编号 |
| `transaction_mode` | varchar(16) | NOT NULL | 汇款方式 |
| `country_code` | varchar(6) |  | 国家code |
| `bank_code` | varchar(20) |  | 银行code |
| `bank_name` | varchar(128) |  | 银行名称 |
| `bank_alias` | varchar(255) |  | 银行别名 |
| `icon` | varchar(255) |  | 图标 |
| `popular_flag` | char |  | 首选项 |
| `enable_flag` | char | NOT NULL | Y：可用，N：不可用 |
| `sort_no` | int(4) |  | sort no |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_t_bank_info` 唯一 (transaction_mode, country_code, bank_code)
- 索引:
  - `idx_country_bank` (country_code, bank_name)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

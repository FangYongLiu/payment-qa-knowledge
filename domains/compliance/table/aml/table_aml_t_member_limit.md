---
id: tbl_aml_t_member_limit
object_type: Table
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (aml schema) 2026-06-25
tags:
- aml
- aml
- t_member_limit
subdomain: aml
module: null
sensitivity: normal
name: 会员限额限次(t_member_limit)
aliases:
- t_member_limit
related_services:
- svc_aml
related_scenarios: []
---
# 会员限额限次(t_member_limit)

## 用途
会员限额限次。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | 主键 |
| `id_no` | varchar(20) |  | 证件号(eid/country+passport),防止passport重复，前面加国家 |
| `kyc_type` | varchar(20) |  | kyc类型 |
| `fund_direction` | varchar(5) |  | 资金方向IN/OUT |
| `single_limit` | decimal(15,4) |  | 单笔限额 |
| `daily_count` | int |  | 日限次 |
| `daily_amount` | decimal(15,4) |  | 日限额 |
| `monthly_count` | int |  | 月限次 |
| `monthly_amount` | decimal(15,4) |  | 月限额 |
| `balance_limit` | decimal(15,4) |  | 余额限制 |
| `currency` | char(3) |  | 币种 |
| `status` | varchar(10) |  | 状态 |
| `member_type` | varchar(20) |  | member type |
| `operator` | varchar(32) |  | Operator |
| `extension` | varchar(255) |  | 扩展字段 |
| `create_time` | timestamp(3) |  | 创建时间 |
| `update_time` | timestamp(3) |  | 修改时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_id_no` (id_no)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

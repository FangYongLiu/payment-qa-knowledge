---
id: tbl_aml_t_member_report
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
- t_member_report
subdomain: aml
module: null
sensitivity: normal
name: 会员反洗钱报告(t_member_report)
aliases:
- t_member_report
related_services:
- svc_aml
related_scenarios: []
---
# 会员反洗钱报告(t_member_report)

## 用途
会员反洗钱报告。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `member_id` | varchar(32) | PK / NOT NULL | 会员ID |
| `aml_sign` | varchar(10) |  | 反洗钱标签 |
| `aml_type` | varchar(32) | 默认 '' | 反洗钱类型 |
| `random_charge_card` | varchar(255) |  | Random_Charge可信卡 |
| `create_time` | timestamp |  | 创建时间 |
| `update_time` | timestamp |  | 更新时间 |

## 主键 / 索引
- 主键:(`member_id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

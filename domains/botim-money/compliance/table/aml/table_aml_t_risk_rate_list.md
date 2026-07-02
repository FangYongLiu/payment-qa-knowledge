---
id: tbl_aml_t_risk_rate_list
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
- t_risk_rate_list
subdomain: aml
module: null
sensitivity: normal
name: 风险评级名单库(t_risk_rate_list)
aliases:
- t_risk_rate_list
related_services:
- svc_aml
related_scenarios: []
---
# 风险评级名单库(t_risk_rate_list)

## 用途
风险评级名单库。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | 主键 |
| `list_library` | varchar(50) | NOT NULL | 名单库 |
| `list_value` | varchar(200) | NOT NULL | 名单值 |
| `status` | char | NOT NULL | 状态 1有效 0无效 |
| `create_time` | timestamp(3) | NOT NULL | 创建时间 |
| `update_time` | timestamp(3) | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_list_library` (list_library)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

---
id: tbl_aml_t_wps_control
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
- t_wps_control
subdomain: aml
module: null
sensitivity: normal
name: wps控制请求(t_wps_control)
aliases:
- t_wps_control
related_services:
- svc_aml
related_scenarios: []
---
# wps控制请求(t_wps_control)

## 用途
wps控制请求。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | 主键 |
| `member_id` | varchar(20) |  | 会员id |
| `salary` | decimal(15,4) |  | 工资 |
| `currency` | char(3) |  | 币种 |
| `operate_type` | varchar(20) |  | 操作类型 |
| `extension` | varchar(255) |  | 扩展字段 |
| `create_time` | timestamp(3) |  | 创建时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_member_id` (member_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

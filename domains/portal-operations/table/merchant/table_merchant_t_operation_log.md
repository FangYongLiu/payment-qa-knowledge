---
id: tbl_merchant_t_operation_log
object_type: Table
domain: portal-operations
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (merchant schema) 2026-06-25
tags:
- merchant
- merchant
- t_operation_log
subdomain: merchant
module: null
sensitivity: normal
name: 操作日志(t_operation_log)
aliases:
- t_operation_log
related_services:
- svc_merchant
related_scenarios: []
---
# 操作日志(t_operation_log)

## 用途
操作日志。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | 主键 |
| `merchant_mid` | varchar(32) | NOT NULL | 商户mid |
| `staff_mid` | varchar(32) | NOT NULL | 员工id |
| `staff_name` | varchar(200) | NOT NULL | 员工姓名 |
| `operation` | varchar(100) | NOT NULL | 操作 |
| `operation_time` | timestamp | NOT NULL | 操作时间 |
| `remark` | varchar(500) |  | 备注 |
| `created_time` | timestamp | NOT NULL | 创建时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

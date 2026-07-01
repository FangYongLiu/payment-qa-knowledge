---
id: tbl_merchant_t_common_dict
object_type: Table
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (merchant schema) 2026-06-25
tags:
- merchant
- merchant
- t_common_dict
subdomain: merchant
module: null
sensitivity: normal
name: Dict table(t_common_dict)
aliases:
- t_common_dict
related_services:
- svc_merchant
related_scenarios: []
---
# Dict table(t_common_dict)

## 用途
Dict table。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | ID |
| `dict_type` | varchar(32) | NOT NULL | Dict type |
| `dict_language` | varchar(20) | NOT NULL / 默认 'EN' | Language |
| `code` | varchar(20) | NOT NULL | Dict code |
| `name` | varchar(255) | NOT NULL | Dict name |
| `parent_code` | varchar(20) |  | Superior code |
| `parent_codes` | varchar(255) |  | All superior codes |
| `status` | varchar(10) | NOT NULL / 默认 'ENABLE' | Status |
| `sort` | int |  | Sort |
| `description` | varchar(1000) |  | Dict description |
| `created_time` | timestamp |  | Created time |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

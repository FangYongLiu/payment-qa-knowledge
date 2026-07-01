---
id: tbl_ppcenter_t_package_template
object_type: Table
domain: activation
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (ppcenter schema) 2026-06-25
tags:
- ppcenter
- pricing
- t_package_template
subdomain: pricing
module: null
sensitivity: normal
name: 产品模板(t_package_template)
aliases:
- t_package_template
related_services:
- svc_ppcenter
related_scenarios: []
---
# 产品模板(t_package_template)

## 用途
产品模板。属 ppcenter 库,由 [[svc_ppcenter]] 读写。

## 关联关系
- **所属服务**:[[svc_ppcenter]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC |  |
| `template_name` | varchar(64) | NOT NULL | 模板名称 |
| `status` | char | NOT NULL | Y表示有效 |
| `memo` | varchar(512) |  | 备注 |
| `gmt_create` | timestamp | NOT NULL | 创建时间 |
| `gmt_modify` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 修改时间 |
| `gmt_effective` | timestamp | NOT NULL | 生效时间 |
| `gmt_invalid` | timestamp | NOT NULL | 失效时间 |
| `effective_duration` | varchar(16) | NOT NULL | 有效周期 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

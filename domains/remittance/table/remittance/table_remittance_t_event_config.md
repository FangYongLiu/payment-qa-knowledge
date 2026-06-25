---
id: tbl_remittance_t_event_config
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
- t_event_config
subdomain: remittance
module: null
sensitivity: normal
name: 事件配置(t_event_config)
aliases:
- t_event_config
related_services:
- svc_remittance
related_scenarios: []
---
# 事件配置(t_event_config)

## 用途
事件配置。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | 主键 |
| `event_code` | varchar(64) | NOT NULL | 事件CODE |
| `event_name` | varchar(100) | NOT NULL | 事件名称 |
| `event_content` | varchar(100) | NOT NULL | 事件内容 |
| `match_key` | varchar(100) |  | 匹配关键字;如订单状态 |
| `match_sub_key` | varchar(100) |  | 匹配子关键字;如订单字状态 |
| `match_expression` | varchar(200) |  | 其他匹配规则 |
| `enable_flag` | char |  | 有效标记;Y/N |
| `memo` | varchar(100) |  | 备注 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |
| `extension` | varchar(150) |  | extension |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

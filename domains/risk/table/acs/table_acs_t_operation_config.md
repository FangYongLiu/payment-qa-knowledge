---
id: tbl_acs_t_operation_config
object_type: Table
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (acs schema) 2026-06-25
tags:
- acs
- acs
- t_operation_config
subdomain: acs
module: null
sensitivity: normal
name: 运营配置记录表(t_operation_config)
aliases:
- t_operation_config
related_services:
- svc_acs
related_scenarios: []
---
# 运营配置记录表(t_operation_config)

## 用途
运营配置记录表。属 acs 库,由 [[svc_acs]] 读写。

## 关联关系
- **所属服务**:[[svc_acs]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `OPERATION_CONFIG_ID` | decimal(8) | PK / NOT NULL | 配置ID |
| `MERCHANT_ID` | varchar(16) |  | 商户ID |
| `CONFIG_TEMPLATE_ID` | decimal(8) |  | 配置模版ID |
| `INVALID_TIME` | timestamp | NOT NULL | 生效时间 |
| `EXPIRED_TIME` | timestamp | NOT NULL | 失效时间 |
| `GMT_CREATE` | timestamp | NOT NULL | 创建时间 |
| `GMT_MODIFY` | timestamp | NOT NULL | 修改时间 |
| `MEMO` | varchar(256) |  | 备注 |

## 主键 / 索引
- 主键:(`OPERATION_CONFIG_ID`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

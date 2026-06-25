---
id: tbl_acs_t_gateway_api_group_relation
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
- t_gateway_api_group_relation
subdomain: acs
module: null
sensitivity: normal
name: 网关API组关联(t_gateway_api_group_relation)
aliases:
- t_gateway_api_group_relation
related_services:
- svc_acs
related_scenarios: []
---
# 网关API组关联(t_gateway_api_group_relation)

## 用途
网关API组关联。属 acs 库,由 [[svc_acs]] 读写。

## 关联关系
- **所属服务**:[[svc_acs]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `RELATION_ID` | bigint | PK / AUTO_INC | 关联ID |
| `API_CONFIG_ID` | bigint | NOT NULL | API配置ID |
| `API_GROUP_ID` | bigint | NOT NULL | API分组ID |
| `GMT_CREATE` | timestamp | NOT NULL | 创建时间 |
| `GMT_MODIFIED` | timestamp | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`RELATION_ID`)
- 唯一约束:
  - `U_GATEWAY_API_GROUP_RELATION_BK` 唯一 (API_CONFIG_ID, API_GROUP_ID)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

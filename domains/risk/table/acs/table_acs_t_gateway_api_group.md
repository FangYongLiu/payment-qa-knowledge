---
id: tbl_acs_t_gateway_api_group
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
- t_gateway_api_group
subdomain: acs
module: null
sensitivity: normal
name: 网关API组(t_gateway_api_group)
aliases:
- t_gateway_api_group
related_services:
- svc_acs
related_scenarios: []
---
# 网关API组(t_gateway_api_group)

## 用途
网关API组。属 acs 库,由 [[svc_acs]] 读写。

## 关联关系
- **所属服务**:[[svc_acs]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `GROUP_ID` | bigint | PK / AUTO_INC | 分组ID |
| `GROUP_CODE` | varchar(64) | NOT NULL | 分组编码 |
| `GROUP_NAME` | varchar(128) | NOT NULL | 分组名称 |
| `ENABLE_FLAG` | char | NOT NULL | 启用标识：Y=启用，N=停用 |
| `EXTENSION` | varchar(1024) |  | 扩展参数 |
| `MEMO` | varchar(512) |  | 备注 |
| `GMT_CREATE` | timestamp | NOT NULL | 创建时间 |
| `GMT_MODIFIED` | timestamp | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`GROUP_ID`)
- 唯一约束:
  - `U_GATEWAY_API_GROUP_GC` 唯一 (GROUP_CODE)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

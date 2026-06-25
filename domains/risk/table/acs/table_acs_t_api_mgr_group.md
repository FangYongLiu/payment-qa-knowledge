---
id: tbl_acs_t_api_mgr_group
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
- t_api_mgr_group
subdomain: acs
module: null
sensitivity: normal
name: 接口分组维护(t_api_mgr_group)
aliases:
- t_api_mgr_group
related_services:
- svc_acs
related_scenarios: []
---
# 接口分组维护(t_api_mgr_group)

## 用途
接口分组维护。属 acs 库,由 [[svc_acs]] 读写。

## 关联关系
- **所属服务**:[[svc_acs]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `API_GROUP_ID` | decimal(8) | PK / NOT NULL | PK,由序列SEQ_API_MGR_GROUP生成 |
| `API_GROUP_NAME` | varchar(40) | NOT NULL | 接口组名称 |
| `API_GROUP_CODE` | varchar(100) | NOT NULL | 接口组编码 |
| `STATUS` | decimal(8) | NOT NULL / 默认 1 | 状态，0:实效，1:有效 |
| `REMARK` | varchar(400) |  | 父ID |
| `GROUP_PARENT_ID` | decimal(8) |  |  |
| `CREATE_TIME` | timestamp | NOT NULL | 创建时间 |
| `UPDATE_TIME` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`API_GROUP_ID`)
- 唯一约束:
  - `UK_T_API_MGR_GROUP_CODE` 唯一 (API_GROUP_CODE)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

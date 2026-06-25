---
id: tbl_acs_t_api_mgr
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
- t_api_mgr
subdomain: acs
module: null
sensitivity: normal
name: 接口管理维护(t_api_mgr)
aliases:
- t_api_mgr
related_services:
- svc_acs
related_scenarios: []
---
# 接口管理维护(t_api_mgr)

## 用途
接口管理维护。属 acs 库,由 [[svc_acs]] 读写。

## 关联关系
- **所属服务**:[[svc_acs]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `API_ID` | decimal(8) | PK / NOT NULL | PK,由序列SEQ_API_MGR生成 |
| `API_CODE` | varchar(40) | NOT NULL | 接口代码 |
| `API_NAME` | varchar(40) | NOT NULL | 接口名 |
| `STATUS` | decimal(8) |  | 状态 |
| `VERSION` | varchar(10) |  | 版本号 |
| `INNER_PRD_CODE` | varchar(40) |  | 内部产品码 |
| `DES` | varchar(100) |  | 接口描述 |
| `REMARK` | varchar(400) |  | 备注 |
| `CREATE_TIME` | timestamp | NOT NULL | 创建时间 |
| `EXT` | varchar(400) |  | 扩展字段 |
| `EXPRESSION` | varchar(200) |  | API匹配表达式 |
| `API_TYPE` | varchar(2) | NOT NULL / 默认 '1' | 接口类型（0公共 1 资金托管 2 B2C） |
| `API_GROUP_ID` | decimal(8) |  | 接口分组ID |

## 主键 / 索引
- 主键:(`API_ID`)
- 索引:
  - `I_T_API_MGR_CODE` (API_CODE)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

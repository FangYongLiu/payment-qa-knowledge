---
id: tbl_acs_t_reffer_list
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
- t_reffer_list
subdomain: acs
module: null
sensitivity: normal
name: 商户黑白名单(t_reffer_list)
aliases:
- t_reffer_list
related_services:
- svc_acs
related_scenarios: []
---
# 商户黑白名单(t_reffer_list)

## 用途
商户黑白名单。属 acs 库,由 [[svc_acs]] 读写。

## 关联关系
- **所属服务**:[[svc_acs]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `ID` | bigint | PK / AUTO_INC |  |
| `MERCHANT_ID` | varchar(25) | NOT NULL | 商户id |
| `REFFERS` | varchar(1024) | NOT NULL | IP或域名通配符  以逗号,分割 |
| `LIST_TYPE` | char | NOT NULL | 名单类型：0 黑名单 1 白名单 |
| `STATUE` | char | NOT NULL | 状态: 0 失效 1 生效 |
| `EXT1` | varchar(40) |  | 扩展1 |
| `EXT2` | varchar(40) |  | 扩展2 |
| `CREATE_TIME` | timestamp | NOT NULL | 创建时间 |
| `LAST_MODIFIED_TIME` | timestamp | NOT NULL | 最后更新时间 |

## 主键 / 索引
- 主键:(`ID`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

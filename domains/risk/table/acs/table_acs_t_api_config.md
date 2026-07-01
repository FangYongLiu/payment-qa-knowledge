---
id: tbl_acs_t_api_config
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
- t_api_config
subdomain: acs
module: null
sensitivity: normal
name: API配置，配置表，1000行(t_api_config)
aliases:
- t_api_config
related_services:
- svc_acs
related_scenarios: []
---
# API配置，配置表，1000行(t_api_config)

## 用途
API配置，配置表，1000行。属 acs 库,由 [[svc_acs]] 读写。

## 关联关系
- **所属服务**:[[svc_acs]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `API_CODE` | varchar(64) | PK / NOT NULL | API代码 |
| `API_NAME` | varchar(100) | NOT NULL | API名称 |
| `APP_CODE` | varchar(30) | NOT NULL | APP代码，与dubbo注册api的version相同 |
| `RATE_LIMIT_GROUP` | varchar(30) | NOT NULL | 限流分组 |
| `STATUS` | varchar(8) | NOT NULL | 状态，Y=启用，N=停用 |
| `EXTENSION` | varchar(2000) |  | 扩展信息 |
| `GMT_CREATE` | timestamp | NOT NULL | 创建时间 |
| `GMT_MODIFY` | timestamp | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`API_CODE`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

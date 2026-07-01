---
id: tbl_acs_t_gateway_api_config
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
- t_gateway_api_config
subdomain: acs
module: null
sensitivity: normal
name: 网关API(t_gateway_api_config)
aliases:
- t_gateway_api_config
related_services:
- svc_acs
related_scenarios: []
---
# 网关API(t_gateway_api_config)

## 用途
网关API。属 acs 库,由 [[svc_acs]] 读写。

## 关联关系
- **所属服务**:[[svc_acs]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `CONFIG_ID` | bigint | PK / AUTO_INC | 配置ID |
| `GATEWAY_TYPE` | varchar(10) | NOT NULL | 网关类型：CGS=客户端网关，SGS=服务端网关 |
| `API_CODE` | varchar(100) | NOT NULL | API编码 |
| `API_NAME` | varchar(100) | NOT NULL | API名称 |
| `APP_CODE` | varchar(50) | NOT NULL | APP编码 |
| `RATE_LIMIT_GROUP` | bigint | NOT NULL | 限流分组ID |
| `ENABLE_FLAG` | char | NOT NULL | 状态：Y=启用，N=停用 |
| `EXTENSION` | varchar(500) |  | extension param |
| `MEMO` | varchar(200) |  | 备注 |
| `GMT_CREATE` | timestamp | NOT NULL | 创建时间 |
| `GMT_MODIFIED` | timestamp | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`CONFIG_ID`)
- 唯一约束:
  - `U_GATEWAY_API_CONFIG_AC_GT` 唯一 (API_CODE, GATEWAY_TYPE)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

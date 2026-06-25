---
id: tbl_acs_t_gateway_merchant_api_auth
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
- t_gateway_merchant_api_auth
subdomain: acs
module: null
sensitivity: normal
name: 网关商户授权(t_gateway_merchant_api_auth)
aliases:
- t_gateway_merchant_api_auth
related_services:
- svc_acs
related_scenarios: []
---
# 网关商户授权(t_gateway_merchant_api_auth)

## 用途
网关商户授权。属 acs 库,由 [[svc_acs]] 读写。

## 关联关系
- **所属服务**:[[svc_acs]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `AUTH_ID` | bigint | PK / AUTO_INC | 授权ID |
| `MERCHANT_ID` | varchar(20) | NOT NULL | 商户ID |
| `API_GROUP_ID` | bigint | NOT NULL | API分组ID |
| `GMT_EFFECT` | timestamp | NOT NULL | 生效时间 |
| `GMT_EXPIRED` | timestamp | NOT NULL | 失效时间 |
| `ENABLE_FLAG` | char | NOT NULL | 启用标识：Y=启用，N=停用 |
| `EXTENSION` | varchar(1024) |  | 扩展参数 |
| `MEMO` | varchar(1024) |  | 备注 |
| `GMT_CREATE` | timestamp | NOT NULL | 创建时间 |
| `GMT_MODIFIED` | timestamp | NOT NULL | 修改时间 |
| `PACKAGE_CODE` | varchar(64) |  | package code |

## 主键 / 索引
- 主键:(`AUTH_ID`)
- 唯一约束:
  - `uk_mid_agid_pc_ef_ex` 唯一 (MERCHANT_ID, API_GROUP_ID, PACKAGE_CODE, GMT_EFFECT, GMT_EXPIRED)
- 索引:
  - `I_GATEWAY_MER_API_AUTH_MID` (MERCHANT_ID)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

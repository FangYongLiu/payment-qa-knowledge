---
id: tbl_acs_t_merchant_api_auth
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
- t_merchant_api_auth
subdomain: acs
module: null
sensitivity: normal
name: 商户服务码映射关系(t_merchant_api_auth)
aliases:
- t_merchant_api_auth
related_services:
- svc_acs
related_scenarios: []
---
# 商户服务码映射关系(t_merchant_api_auth)

## 用途
商户服务码映射关系。属 acs 库,由 [[svc_acs]] 读写。

## 关联关系
- **所属服务**:[[svc_acs]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `AUTH_ID` | decimal(8) | PK / NOT NULL | 主键，由SEQ_API_AUTH生成 |
| `API_ID` | decimal(8) | NOT NULL | 外键 |
| `MERCHANT_ID` | varchar(20) | NOT NULL | 商户ID |
| `OUTER_CODE` | varchar(20) |  | 外部服务码 |
| `NEED_OUTCODE` | decimal(8) |  | 是否需要服务码 |
| `PART_ACCOUNT` | varchar(40) |  | 参与方账号 |
| `VALID_DATE` | timestamp |  | 有效期 |
| `STATUS` | decimal(8) |  | 状态 |
| `PART_ACC_ROLE` | varchar(20) |  | 账号角色 |
| `EXT` | varchar(400) |  | 扩展字段 |
| `REMARK` | varchar(400) |  | 备注 |
| `CREATE_TIME` | timestamp | NOT NULL | 创建时间 |
| `LAST_MODIFIED_TIME` | timestamp | NOT NULL | 最后更新时间 |
| `IP_LIST` | varchar(100) |  | 商户接口IP白名单 |

## 主键 / 索引
- 主键:(`AUTH_ID`)
- 唯一约束:
  - `UI_T_MERCHANT_API_MER` 唯一 (MERCHANT_ID, API_ID, OUTER_CODE)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

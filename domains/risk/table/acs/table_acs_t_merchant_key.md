---
id: tbl_acs_t_merchant_key
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
- t_merchant_key
subdomain: acs
module: null
sensitivity: normal
name: 管理商户密钥信息(t_merchant_key)
aliases:
- t_merchant_key
related_services:
- svc_acs
related_scenarios: []
---
# 管理商户密钥信息(t_merchant_key)

## 用途
管理商户密钥信息。属 acs 库,由 [[svc_acs]] 读写。

## 关联关系
- **所属服务**:[[svc_acs]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `ID` | decimal(8) | PK / NOT NULL |  |
| `MERCHANT_ID` | varchar(20) | NOT NULL | 商户id |
| `PLATFORM_TYPE` | decimal(8) |  | 平台类型 |
| `CERTIFICATE` | varchar(4000) |  | 证书内容 |
| `CERT_TYPE` | decimal(8) |  | 证书类型 |
| `CERT_FORMAT` | varchar(40) |  | 证书格式 |
| `ALGORITHM` | varchar(20) | NOT NULL | 加密算法 |
| `VERSION` | varchar(20) |  | 版本号 |
| `VALID_DATE` | timestamp |  | 有效期 |
| `EXT` | varchar(400) |  | 扩展字段 |
| `REMARK` | varchar(400) |  | 备注 |
| `CREATE_TIME` | timestamp |  | 创建时间 |
| `LAST_MODIFIED_TIME` | timestamp |  | 最后更新时间 |

## 主键 / 索引
- 主键:(`ID`)
- 唯一约束:
  - `UK_MERCHANT_KEY` 唯一 (MERCHANT_ID, ALGORITHM, VERSION, CERT_TYPE)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

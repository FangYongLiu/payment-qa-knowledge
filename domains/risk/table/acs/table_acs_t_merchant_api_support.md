---
id: tbl_acs_t_merchant_api_support
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
- t_merchant_api_support
subdomain: acs
module: null
sensitivity: normal
name: 商户接口秘钥关系(t_merchant_api_support)
aliases:
- t_merchant_api_support
related_services:
- svc_acs
related_scenarios: []
---
# 商户接口秘钥关系(t_merchant_api_support)

## 用途
商户接口秘钥关系。属 acs 库,由 [[svc_acs]] 读写。

## 关联关系
- **所属服务**:[[svc_acs]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `SUPPORT_ID` | decimal(15) | PK / NOT NULL | 主键 |
| `API_ID` | decimal(15) | NOT NULL | 接口ID |
| `MERCHANT_ID` | varchar(32) | NOT NULL | 商户号 |
| `SIGN_VERSION` | varchar(20) | NOT NULL | 秘钥版本号 |
| `ALGORITHM` | varchar(20) |  | 秘钥类型 |
| `STATUS` | varchar(2) | NOT NULL | 状态 |
| `GMT_CREATE` | timestamp | NOT NULL | 创建时间 |
| `GMT_MODIFIED` | timestamp | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`SUPPORT_ID`)
- 索引:
  - `I_MERID_MERCHANT_ID_KEY` (API_ID, MERCHANT_ID)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

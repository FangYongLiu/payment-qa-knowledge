---
id: tbl_acs_t_withhold_auth
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
- t_withhold_auth
subdomain: acs
module: null
sensitivity: normal
name: 委托代扣授权(t_withhold_auth)
aliases:
- t_withhold_auth
related_services:
- svc_acs
related_scenarios: []
---
# 委托代扣授权(t_withhold_auth)

## 用途
委托代扣授权。属 acs 库,由 [[svc_acs]] 读写。

## 关联关系
- **所属服务**:[[svc_acs]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `ID` | decimal(8) | PK / NOT NULL | 主键，由SEQ_WITHHOLD生成 |
| `MERCHANT_ID` | varchar(20) | NOT NULL | 商户会员ID |
| `AUTHORIZED_MID` | varchar(20) | NOT NULL | 被授权会员ID |
| `STATUS` | decimal(8) | NOT NULL | 状态 |
| `REMARK` | varchar(50) |  | 备注 |
| `EXT` | varchar(400) |  | 扩展字段 |
| `CREATE_TIME` | timestamp |  | 创建时间 |
| `LAST_MODIFIED_TIME` | timestamp |  | 最后更新时间 |
| `AUTH_TYPE` | varchar(20) |  | 授权类型（ALL:所有 ACCOUNT:账户 CARD：银行卡） |
| `AUTH_SUB_TYPE` | varchar(20) |  | 授权子类型（账户类型：ALL：所有账户 SAVING_POT:存钱罐 BASIS:基本户 银行卡：ALL：所有卡） |
| `CARD_ID` | varchar(50) |  | 银行卡 |
| `QUOTA` | varchar(50) |  | 额度 |
| `EFFECT_TIME` | timestamp |  | 生效时间 |
| `INVALID_TIME` | timestamp |  | 失效时间 |
| `PRODUCT_CODE` | varchar(20) |  | 产品号 |
| `DAY_QUOTA` | varchar(50) |  | 日累计额度 |

## 主键 / 索引
- 主键:(`ID`)
- 索引:
  - `I_T_WITHHOLD_AUTH_MER` (MERCHANT_ID)
  - `I_WITHHOLD_AUTH_MID` (AUTHORIZED_MID)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

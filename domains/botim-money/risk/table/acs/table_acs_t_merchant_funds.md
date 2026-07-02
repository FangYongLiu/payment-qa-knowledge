---
id: tbl_acs_t_merchant_funds
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
- t_merchant_funds
subdomain: acs
module: null
sensitivity: normal
name: 商户垫资配置(t_merchant_funds)
aliases:
- t_merchant_funds
related_services:
- svc_acs
related_scenarios: []
---
# 商户垫资配置(t_merchant_funds)

## 用途
商户垫资配置。属 acs 库,由 [[svc_acs]] 读写。

## 关联关系
- **所属服务**:[[svc_acs]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `ID` | decimal(15) | PK / NOT NULL |  |
| `MERCHANT_ID` | varchar(32) | NOT NULL | 商户ID |
| `FUNDS_TYPE` | varchar(8) | NOT NULL | 资金类型 |
| `FUNDS_SOURCE` | char | NOT NULL | 资金来源,0：配置值,1：实时取值 |
| `DIRECT` | char | NOT NULL | 资金方向, +/- |
| `FUNDS_AMOUNT` | decimal(16,2) |  | 可垫资金额 |
| `ACCOUNT_NO` | varchar(32) |  | 垫资账户号 |
| `THIRD_PAYMENT` | char |  | 是否支持第三方垫资账户 |
| `THIRD_MEMBER` | varchar(32) |  | 第三方垫资商户号 |
| `STATUS` | char | NOT NULL | 状态 |
| `GMT_CREATE` | timestamp | NOT NULL | 创建时间 |
| `GMT_MODIFIED` | timestamp | NOT NULL | 修改时间 |
| `BIZ_PRODUCT_CODE` | varchar(128) |  | 业务产品码 |
| `IS_SINGLE` | char | NOT NULL / 默认 '0' | 是否独享垫资额度，0:否；1:是 |
| `PRIORITY` | decimal |  | 优先级 |
| `INVALID_TIME` | timestamp |  | 生效时间 |
| `EXPIRE_TIME` | timestamp |  | 失效时间 |
| `WHITE_CHANNEL_CODE` | varchar(50) |  | 渠道白名单 |

## 主键 / 索引
- 主键:(`ID`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

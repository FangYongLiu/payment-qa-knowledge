---
id: tbl_acs_t_merchant_fo_setting
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
- t_merchant_fo_setting
subdomain: acs
module: null
sensitivity: normal
name: 商户出款配置(t_merchant_fo_setting)
aliases:
- t_merchant_fo_setting
related_services:
- svc_acs
related_scenarios: []
---
# 商户出款配置(t_merchant_fo_setting)

## 用途
商户出款配置。属 acs 库,由 [[svc_acs]] 读写。

## 关联关系
- **所属服务**:[[svc_acs]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `ID` | decimal(15) | PK / NOT NULL |  |
| `MERCHANT_ID` | varchar(32) | NOT NULL | 商户号 |
| `DEFINE_VALUE` | decimal(16,2) |  | 自定义调整阀值 |
| `BIZ_PRODUCT_CODE` | varchar(32) | NOT NULL | 业务产品码 |
| `FUNDOUT_GRADE_TYPE` | varchar(32) | NOT NULL | 支持调整的出款类型,快速/普通/全部 |
| `AUTO_ADJUST` | char | NOT NULL | 是否支持自动调整出款类型 |
| `GMT_CREATE` | timestamp | NOT NULL | 创建时间 |
| `GMT_MODIFIED` | timestamp | NOT NULL | 修改时间 |
| `ADVANCE_MERCHANT` | char |  | 是否垫资商户 |
| `TYPE` | char | NOT NULL / 默认 '0' | 0:商户垫资，1:B2C，2商户垫资加B2C |

## 主键 / 索引
- 主键:(`ID`)
- 唯一约束:
  - `UK_MERID_PROCUCTCODE_KEY` 唯一 (MERCHANT_ID, BIZ_PRODUCT_CODE)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

---
id: tbl_acs_t_merchant_setting
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
- t_merchant_setting
subdomain: acs
module: null
sensitivity: normal
name: 商户配置表(t_merchant_setting)
aliases:
- t_merchant_setting
related_services:
- svc_acs
related_scenarios: []
---
# 商户配置表(t_merchant_setting)

## 用途
商户配置表。属 acs 库,由 [[svc_acs]] 读写。

## 关联关系
- **所属服务**:[[svc_acs]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `ID` | decimal(16) | PK / NOT NULL | 主键ID |
| `MERCHANT_ID` | varchar(100) |  | 商户号 |
| `PARAM_KEY` | varchar(128) |  | 参数名称 |
| `PARAM_VALUE` | varchar(8000) |  | 参数内容 |
| `CREATE_TIME` | timestamp | 默认 CURRENT_TIMESTAMP | 创建时间 |
| `LAST_UPDATED_TIME` | timestamp | 默认 CURRENT_TIMESTAMP | 最后更新时间 |

## 主键 / 索引
- 主键:(`ID`)
- 唯一约束:
  - `UK_MERCHANT_SETTING` 唯一 (MERCHANT_ID, PARAM_KEY)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

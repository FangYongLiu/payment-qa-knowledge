---
id: tbl_pbsdb_tb_pbs_price_strategy
object_type: Table
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (pbsdb schema) 2026-06-25
tags:
- pbsdb
- pricing
- tb_pbs_price_strategy
subdomain: pricing
module: null
sensitivity: normal
name: 定价策略表(tb_pbs_price_strategy)
aliases:
- tb_pbs_price_strategy
related_services:
- svc_pbs
related_scenarios: []
---
# 定价策略表(tb_pbs_price_strategy)

## 用途
定价策略表。属 pbsdb 库,由 [[svc_pbs]] 读写。

## 关联关系
- **所属服务**:[[svc_pbs]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `PRICE_STRATEGY_ID` | decimal(15) | PK / NOT NULL | 主键ID |
| `NAME` | varchar(50) | NOT NULL | 定价名称 |
| `STRATEGY_SCOPE` | char |  | 策略范围 |
| `POSTING_CODE` | varchar(32) | NOT NULL | 业务子代码 |
| `PT_ID` | varchar(32) |  | 会员PTID |
| `TAKEN_ON` | char |  | S-收款方 F-付款方 |
| `PRODUCT_CODE` | varchar(32) |  | 产品编码,此字段为预留字段，暂不起作用 |
| `MEMO` | varchar(300) |  | 备注 |
| `EXPIREDATE` | timestamp | NOT NULL | 失效时间 |
| `VALIDDATE` | timestamp | NOT NULL | 生效时间 |
| `STATUS` | char | NOT NULL | C-创建 A-可用 D-废弃 |
| `GMT_CREATE` | timestamp | NOT NULL | 创建时间 |
| `GMT_MODIFIED` | timestamp |  | 修改时间 |
| `CREATE_BY` | varchar(50) | NOT NULL | 创建人 |
| `LAST_REVISED_BY` | varchar(50) |  | 最后修改人 |

## 主键 / 索引
- 主键:(`PRICE_STRATEGY_ID`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

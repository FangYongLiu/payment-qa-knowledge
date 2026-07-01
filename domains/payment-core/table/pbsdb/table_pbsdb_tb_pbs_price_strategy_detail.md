---
id: tbl_pbsdb_tb_pbs_price_strategy_detail
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
- tb_pbs_price_strategy_detail
subdomain: pricing
module: null
sensitivity: normal
name: 定价策略明细表(tb_pbs_price_strategy_detail)
aliases:
- tb_pbs_price_strategy_detail
related_services:
- svc_pbs
related_scenarios: []
---
# 定价策略明细表(tb_pbs_price_strategy_detail)

## 用途
定价策略明细表。属 pbsdb 库,由 [[svc_pbs]] 读写。

## 关联关系
- **所属服务**:[[svc_pbs]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `PRICE_STRATEGY_DETAIL_ID` | decimal(15) | PK / NOT NULL | 主键ID |
| `STRATEGY_SCOPE` | char |  | 策略应用范围,表示本策略的适用范围是 G-全局 如果为空则为个体 |
| `PRICE_STRATEGY_ID` | decimal(15) | NOT NULL | 定价策略ID |
| `CRITERION_ID` | decimal(15) |  | 约束ID |
| `PRICE_CAL_ID` | decimal(15) | NOT NULL | 价格策略计算ID |
| `BILL_STRATEGY_ID` | decimal(15) | NOT NULL | 账单生成策略 |
| `CHANNEL` | varchar(32) |  | 渠道 |
| `VALIDDATE` | timestamp |  | 生效时间，必须大于等于定价策略的生效时间，小于定价策略中的失效时间如果为空，则沿用定价策略的生效时间 |
| `EXPIREDATE` | timestamp |  | 失效时间，必须小于等于定价策略的失效时间，大于定价策略中的生效时间如果为空，则沿用定价策略的失效时间 |
| `MEMO` | varchar(300) |  | 备注 |
| `STATUS` | char | NOT NULL | C-创建 A-可用 D-废弃 |
| `LAST_REVISED_BY` | varchar(50) |  | 最后修改人 |
| `CREATE_BY` | varchar(50) | NOT NULL | 创建人 |
| `GMT_MODIFIED` | timestamp |  | 最后修改时间 |
| `GMT_CREATE` | timestamp | NOT NULL | 创建时间 |

## 主键 / 索引
- 主键:(`PRICE_STRATEGY_DETAIL_ID`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

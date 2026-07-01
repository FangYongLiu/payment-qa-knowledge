---
id: tbl_pbsdb_tb_pbs_price_strategy_param
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
- tb_pbs_price_strategy_param
subdomain: pricing
module: null
sensitivity: normal
name: 定价策略明细表(tb_pbs_price_strategy_param)
aliases:
- tb_pbs_price_strategy_param
related_services:
- svc_pbs
related_scenarios: []
---
# 定价策略明细表(tb_pbs_price_strategy_param)

## 用途
定价策略明细表。属 pbsdb 库,由 [[svc_pbs]] 读写。

## 关联关系
- **所属服务**:[[svc_pbs]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `PRICE_STRATEGY_PARAM_ID` | decimal(15) | PK / NOT NULL | 主键ID |
| `PRICE_STRATEGY_ID` | decimal(15) | NOT NULL | 定价策略ID |
| `PRICE_CAL_ID` | decimal(15) | NOT NULL | 价格策略计算ID |
| `CHANNEL_MODE` | varchar(32) |  | 渠道类型 |
| `CURRENCY` | varchar(6) |  | 币种,如AED |
| `VALIDDATE` | timestamp |  | 生效时间，必须大于等于定价策略的生效时间，小于定价策略中的失效时间 如果为空，则沿用定价策略的生效时间 |
| `EXPIREDATE` | timestamp |  | 失效时间，必须小于等于定价策略的失效时间，大于定价策略中的生效时间 如果为空，则沿用定价策略的失效时间 |
| `MEMO` | varchar(300) |  | 备注 |
| `STATUS` | char | NOT NULL | C-创建 A-可用 D-废弃 |
| `LAST_REVISED_BY` | varchar(50) |  | 最后修改人 |
| `CREATE_BY` | varchar(50) | NOT NULL | 创建人 |
| `GMT_MODIFIED` | timestamp |  | 修改时间 |
| `GMT_CREATE` | timestamp | NOT NULL | 创建时间 |
| `SCOPE` | char(2) |  | 00 - all 01 - channel_mode |
| `EXT_PARAMS` | varchar(3000) |  | 扩展参数 |
| `STRATEGY_TYPE` | decimal(2) |  | 1-单笔定额 2-阶梯定额 3-单笔费率 4-阶梯费率 5-按比例退费（适用于退款） 6-合同期累计阶梯定额 7-合同期累计阶梯费率 |
| `EXT_CAL_PARAMS` | varchar(3000) |  | 计算费用所需要的参数 |

## 主键 / 索引
- 主键:(`PRICE_STRATEGY_PARAM_ID`)
- 索引:
  - `idx_PRICE_STRATEGY_ID` (PRICE_STRATEGY_ID)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

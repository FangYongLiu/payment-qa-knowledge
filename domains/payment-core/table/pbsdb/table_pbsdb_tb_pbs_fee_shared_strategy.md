---
id: tbl_pbsdb_tb_pbs_fee_shared_strategy
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
- tb_pbs_fee_shared_strategy
subdomain: pricing
module: null
sensitivity: normal
name: 费用分摊策略表(tb_pbs_fee_shared_strategy)
aliases:
- tb_pbs_fee_shared_strategy
related_services:
- svc_pbs
related_scenarios: []
---
# 费用分摊策略表(tb_pbs_fee_shared_strategy)

## 用途
费用分摊策略表。属 pbsdb 库,由 [[svc_pbs]] 读写。

## 关联关系
- **所属服务**:[[svc_pbs]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `FEE_SHARED_STRATEGY_ID` | decimal(15) | PK / NOT NULL | ID |
| `PRICE_STRATEGY_PARAM_ID` | decimal(15) | NOT NULL | 主键ID |
| `FEE_SHARED_MEMBER_ID` | varchar(64) |  | 分摊方的member id,为空表示匹配所有 |
| `FEE_SHARED_PARTY_ROLE` | varchar(10) | NOT NULL | 只支持PAYER和PAYEE两种角色 |
| `PRICE_CAL_ID` | decimal(15) | NOT NULL | 价格策略计算ID |
| `STRATEGY_TYPE` | char | NOT NULL | 策略类型 |
| `EXT_PARAMS` | varchar(3000) |  | 扩展参数 |
| `EXT_CAL_PARAMS` | varchar(3000) |  | 策略扩展 |
| `MEMO` | varchar(300) |  | 备注 |
| `LAST_REVISED_BY` | varchar(50) |  | 最后修改人 |
| `CREATE_BY` | varchar(50) | NOT NULL | 创建人 |
| `GMT_MODIFIED` | timestamp |  | 最后修改时间 |
| `GMT_CREATE` | timestamp | NOT NULL | 创建时间 |

## 主键 / 索引
- 主键:(`FEE_SHARED_STRATEGY_ID`)
- 索引:
  - `IDX_PRICE_STRATE_PARAM_ID` (PRICE_STRATEGY_PARAM_ID)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

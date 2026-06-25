---
id: tbl_pricing_db
object_type: Table
name: 费率配置相关表(ppcenter / pbsdb)
aliases:
- ppcenter
- pbs
- pbsdb
- 费率配置
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:tester/124289264
tags:
- 费率
- 产品模板
- 费率策略
- 定价
related_services:
- svc_ppcenter
- svc_pbs
related_tables:
- tbl_trade_db
- tbl_statement_db
related_scenarios: []
---

# 费率配置相关表(ppcenter / pbsdb)

## 用途
集中存放产品模板、费率定义/配置、产品申请审核、产品包关联,以及 PBS 费率策略与价格计算策略相关数据。涵盖两个库:
- `ppcenter`:产品模板与费率配置
- `pbsdb`:PBS 费率策略

> 这是定价域的**库级速查对象**(多库多表的清单),字段级明细以各表为准;尚无单表独立对象的字段标「待补」。

## 关联关系
- **所属服务**:[[svc_ppcenter]](产品模板/费率配置)、[[svc_pbs]](PBS 费率策略)(= frontmatter `related_services`)。
- **谁读写它**:费率配置在交易计费及账单核算中取数,见 [[tbl_trade_db]]、[[tbl_statement_db]]。
- **哪些场景校验它**:待补(尚无 `related_scenarios`)。
- 导航入口见 [[ts_payment_db_navigation]]。

## 关键列
### ppcenter 费率配置
| 表 | 说明 |
| --- | --- |
| `ppcenter.t_product_template` | 产品模板 |
| `ppcenter.t_calculation_define` | 费率定义 |
| `ppcenter.t_price_cal` | 费率配置 |
| `ppcenter.t_product_apply_order` | 产品申请 |
| `ppcenter.t_product_apply_info` | 申请审核资料 |
| `ppcenter.t_package_define` | 产品包 |
| `ppcenter.t_package_template_relation` | 产品包与产品模板的关联 |

### pbs 费率策略
| 表 | 说明 |
| --- | --- |
| `pbsdb.tb_pbs_price_strategy_unit` | 费率策略 |
| `pbsdb.tb_pbs_price_strategy_param` | 策略详情 |
| `pbsdb.tb_pbs_price_cal` | 价格计算策略 |

各表物理字段定义:待补(原文未提供)。

## 主键 / 索引
待补:原文未提供,以表内主键/外键为准。

## 校验点(QA 关注)
- 产品模板 `t_product_template` 与费率定义 `t_calculation_define`、费率配置 `t_price_cal` 的关联一致性。
- 产品申请 `t_product_apply_order` 与审核资料 `t_product_apply_info` 的对应完整性。
- 产品包 `t_package_define` 通过 `t_package_template_relation` 关联到产品模板的正确性。
- PBS 侧 `tb_pbs_price_strategy_unit` 与 `tb_pbs_price_strategy_param`、`tb_pbs_price_cal` 的策略-参数-计算链路一致。
- 与交易/账单链路的对接:费率配置在交易计费及账单核算中的取数准确性(参见 [[tbl_trade_db]]、[[tbl_statement_db]])。

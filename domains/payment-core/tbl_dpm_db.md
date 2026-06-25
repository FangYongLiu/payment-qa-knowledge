---
id: tbl_dpm_db
object_type: Table
name: 会员账户库 dpm 核心表(dpm)
aliases:
- dpm
- 会员账户库
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:tester/124289264
tags:
- 账户
- 余额
- 会员
- dpm
related_services:
- svc_dpm_accounting
related_tables:
- tbl_member_db
- tbl_trade_db
related_scenarios: []
---

# 会员账户库 dpm 核心表(dpm)

## 用途
`dpm` 为会员账户库,记录会员的外部账户、外部账户分户信息,以及内外部账户的余额变动明细,用于支撑会员账户余额查询与账务核对。归属会员账户体系,余额变动由会员/交易链路驱动。

> 这是 `dpm` 库的**库级速查对象**(多张表的清单),字段级明细以各表为准;尚无单表独立对象的字段标「待补」。

## 关联关系
- **所属服务**:[[svc_dpm_accounting]](= frontmatter `related_services`);相关还有 [[svc_dpm_manager]]、[[svc_dpm_task]](dpm 体系,本侧不重复连边)。
- **谁读写它**:交易链路写入余额变动明细(见 [[tbl_trade_db]]);会员维度联查 [[tbl_member_db]]。
- **哪些场景校验它**:待补(尚无 `related_scenarios`)。
- 导航入口见 [[ts_payment_db_navigation]]。

## 关键列
| 表 | 说明 |
| --- | --- |
| `t_dpm_outer_account` | 会员外部账户信息 |
| `t_dpm_outer_account_subset` | 外部账户分户表 |
| `t_dpm_outer_account_sub_detail` | 外部账户分户账户明细,记录外部账户余额变动明细 |
| `t_dpm_inner_account_detail` | 内部账户余额明细 |

各表物理字段定义:待补(原文未提供)。

## 主键 / 索引
待补:原文未提供。

## 校验点(QA 关注)
- 余额变动场景需核对 `t_dpm_outer_account_sub_detail`(外部账户分户账户明细)与 `t_dpm_inner_account_detail`(内部账户余额明细)是否同步生成对应明细。
- 外部账户(`t_dpm_outer_account`)与其分户(`t_dpm_outer_account_subset`)的关联完整性。
- 会员账户相关查询通常需结合 [[tbl_member_db]] 中的会员/账户信息进行联查校验。
- 交易引发的账户变动应与 [[tbl_trade_db]] 中对应订单/支付记录可对账。

---
id: tbl_tradeii_db
object_type: Table
name: 交易核心库 trade 核心表(trade)
aliases:
- 交易类核心表
- trade db
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:tester/124289264
tags:
- 交易
- 收单
- 退款
- 出款
- 转账
- 充值
- 提现
related_services:
- svc_tradeii
- svc_deposit
related_scenarios: []
related_tables:
- tbl_dpm_db
- tbl_member_db
- tbl_merchant_db
- tbl_pbsdb_db
- tbl_ppcenter_db
- tbl_statement_db
- tbl_trade_leaf_alloc
- tbl_trade_t_acq_trade_order_ext
- tbl_trade_t_compensation_event
- tbl_trade_t_control_order
- tbl_trade_t_market_method
- tbl_trade_t_order_ext
- tbl_trade_t_other_party
- tbl_trade_t_pay_method
- tbl_trade_t_payment_order
- tbl_trade_t_payment_party
- tbl_trade_t_rfd_trade_order_ext
- tbl_trade_t_split_party
- tbl_trade_t_task_config
- tbl_trade_t_trade_batch_order
- tbl_trade_t_trade_order
- tbl_trade_t_trade_order_setting
- tbl_trade_t_trade_status_his
---

# 交易类核心表(acquireii / mhtfundout / transfer / deposit / tradeii / fundout)

## 用途
覆盖交易域核心库表,包含收单、退款、出款、个人转账,以及中台交易(充值、交易、提现)相关的订单与支付信息,用于支付交易全链路数据查询与核对。跨多个物理库(`acquireii` / `mhtfundout` / `transfer` / `deposit` / `tradeii` / `fundout`)。

> 这是交易域的**库级速查对象**(多库多表的清单),字段级明细以各表为准;尚无单表独立对象的字段标「待补」。

## 关联关系
- **所属服务**:中台交易 [[svc_tradeii]]、充值 [[svc_deposit]](= frontmatter `related_services`)。收单(acquireii)、出款(mhtfundout)、转账(transfer)、提现(fundout)对应服务落在其它业务域,待补,本侧不硬连。
- **谁读写它**:账户余额变动落 [[tbl_dpm_db]];会员维度联查 [[tbl_member_db]];商户维度联查 [[tbl_merchant_db]];对账统计见 [[tbl_statementii_db]];计费取数见 [[tbl_ppcenter_db]]、[[tbl_pbsdb_db]]。
- **哪些场景校验它**:待补(尚无 `related_scenarios`)。
- 导航入口见 [[ts_payment_db_navigation]]。

## 关键列
### 交易类
| 表 | 说明 |
| --- | --- |
| `acquireii.t_acquire_order` | 收单交易表 |
| `acquireii.t_payment_info` | 收单支付信息表 |
| `acquireii.t_refund_order` | 收单退款订单表 |
| `mhtfundout.t_fundout_order` | 出款服务订单表 |
| `mhtfundout.t_payment_info` | 出款服务支付信息表 |
| `mhtfundout.t_fundout_account_beneficiary` | 出款服务收款方信息表 |
| `transfer.t_transfer_order` | 个人转账 |

### 中台交易类
| 表 | 说明 |
| --- | --- |
| `deposit.t_deposit_order` | 充值 |
| `tradeii.t_trade_order` | 交易主单 |
| `tradeii.t_order_ext` | 交易订单扩展表 |
| `tradeii.t_payment_order` | 交易支付订单表 |
| `fundout.tt_fundout_order` | 提现 |

各表物理字段定义:待补(原文未提供)。

## 主键 / 索引
待补:原文未提供。

## 校验点(QA 关注)
- 收单链路:`t_acquire_order` 与 `t_payment_info`、`t_refund_order` 的订单关联与状态一致性。
- 出款链路:区分 `mhtfundout.t_fundout_order`(出款服务)与 `fundout.tt_fundout_order`(中台提现)两类不同的出款表。
- 中台交易:`tradeii.t_trade_order`、`t_order_ext`、`t_payment_order` 三表的订单/扩展/支付订单关联。
- 充值与提现分别落库 `deposit.t_deposit_order` 与 `fundout.tt_fundout_order`。
- 个人转账落库 `transfer.t_transfer_order`,与收单/中台交易表区分使用。
- 交易引发的账户余额变动应与 [[tbl_dpm_db]] 明细可对账;计费取数应与 [[tbl_ppcenter_db]]、[[tbl_pbsdb_db]] 费率配置一致。

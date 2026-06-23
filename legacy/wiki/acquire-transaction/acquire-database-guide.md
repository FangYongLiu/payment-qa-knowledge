---
title: 收单交易常用数据库表指南
domain: acquire-transaction
kind: wiki_page
slug: acquire-database-guide
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/997851554
tags: []
---

# 收单交易常用数据库表指南

本页汇总收单交易链路上常用的数据库表及对应查询 SQL，便于在排查交易、订单、鉴权、风控、清算等问题时快速定位数据。配套的应用服务可参考 [[acquire-services-catalog]]。

## 环境与连接说明

- SIM 环境 MySQL 连接详情：http://gitlab.test2pay.com/dba/passwd/blob/master/mysql.md
- 表名格式：`库名.表名`，可直接在对应库中查询。

## 收单与交易订单

- 收单交易表
  ```sql
  select * from acquireii.t_acquire_order;
  ```
- 交易订单
  ```sql
  select * from tradeii.t_trade_order;
  ```

## 收银台与鉴权

- 收银台鉴权方案配置
  ```sql
  select * from cashdesk.t_group_scheme_rel;
  ```
- 收银台鉴权节点
  ```sql
  select * from cashdesk.t_filter_scheme;
  ```

## 风控与会员

- 风控核身规则
  ```sql
  select * from aml.t_identity_rule;
  ```
- 会员信息表
  ```sql
  select * from member.tm_member;
  ```

## 账户与资金

- 外部账户 - 商户 Basic 帐户 - 余额
  ```sql
  select * from dpm.t_dpm_outer_account_subset;
  ```
- 入账流水
  ```sql
  select * from reconciliation.t_fund_flow;
  ```
- 商户提现订单记录
  ```sql
  select * from mhtfundout.t_withdraw_order;
  ```

## 渠道与路由

- 渠道订单
  ```sql
  select * from cmf.tt_cmf_order;
  ```
- 路由渠道
  ```sql
  select * from router.t_channel;
  ```

## 相关参考

- 业务全景与流程：[[acquire-transaction-overview]]
- 支付场景枚举：[[acquire-pay-scene-code]]
- 支付渠道号枚举：[[acquire-pay-channel-no]]
- 应用服务与负责人：[[acquire-services-catalog]]

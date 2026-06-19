---
title: PayBy收单交易数据库速查指南
domain: acquire-transaction
kind: wiki_page
slug: payby-acquire-databases-guide
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:725ad723-2e21-421d-837b-1ac7e8e0fd3a
tags: []
---

# PayBy收单交易数据库速查指南

本页汇总 PayBy 收单交易链路上各核心服务对应的数据库表及常用查询 SQL，便于快速定位订单、鉴权、风控、渠道、清算等环节的数据。相关业务背景见 [[payby-acquire-transaction-overview]]，应用与负责人见 [[payby-acquire-applications-owners]]。

## 数据库连接与文档

- SIM 环境 MySQL 连接详情：`http://gitlab.test2pay.com/dba/passwd/blob/master/mysql.md`

## 核心交易表

| 用途 | 库.表 |
|---|---|
| 收单交易表 | `acquireii.t_acquire_order` |
| 交易订单 | `tradeii.t_trade_order` |

```sql
select * from acquireii.t_acquire_order;
select * from tradeii.t_trade_order;
```

## 收银台与鉴权

- 收银台鉴权方案配置：`cashdesk.t_group_scheme_rel`
- 收银台鉴权节点：`cashdesk.t_filter_scheme`

```sql
select * from cashdesk.t_group_scheme_rel;
select * from cashdesk.t_filter_scheme;
```

## 风控核身

- 风控核身规则：`aml.t_identity_rule`

```sql
select * from aml.t_identity_rule;
```

## 会员与账户

- 会员信息表：`member.tm_member`
- 外部账户-商户 Basic 帐户-余额：`dpm.t_dpm_outer_account_subset`

```sql
select * from member.tm_member;
select * from dpm.t_dpm_outer_account_subset;
```

## 渠道与路由

- 渠道订单：`cmf.tt_cmf_order`
- 路由渠道：`router.t_channel`

```sql
select * from cmf.tt_cmf_order;
select * from router.t_channel;
```

> 渠道维度的取值参见 [[payby-acquire-pay-scene-codes]]。

## 清算与出款

- 入账流水：`reconciliation.t_fund_flow`
- 商户提现订单记录：`mhtfundout.t_withdraw_order`

```sql
select * from reconciliation.t_fund_flow;
select * from mhtfundout.t_withdraw_order;
```

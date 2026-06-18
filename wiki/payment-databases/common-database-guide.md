---
title: 常用数据库指南
domain: payment-databases
kind: wiki_page
slug: common-database-guide
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:tester/124289264
tags: []
---

# 常用数据库指南

本页汇总 PayBy 各业务库及常用表的用途说明，便于 QA 在排查问题、构造测试数据和定位字段时快速找到目标库表。具体字段与样例查询见各分库子页。

## 库与子页索引

- [[tbl_member_db]] —— `member` 会员相关库（会员/认证/操作员/密码/设备绑定/银行卡/实名）
- [[tbl_dpm_db]] —— `dpm` 会员账户库（外部账户、分户、内部账户余额明细）
- [[tbl_acs_db]] —— `acs` 网关库（公私钥、接口权限、接口配置、IP 白名单）
- [[tbl_merchant_db]] —— `merchant` 商户库（商户/门店/员工/账期/定时出款）
- [[tbl_device_db]] —— `device` 设备库（硬件信息、绑定、激活码、申请单、密钥）
- [[tbl_trade_db]] —— 交易类（收单 acquireii、出款 mhtfundout、转账 transfer，以及中台 deposit / tradeii / fundout）
- [[tbl_statement_db]] —— `statementii` 账单库（账期、登记、模板、任务、文件、收单统计）
- [[tbl_pricing_db]] —— 费率配置（`ppcenter` 产品模板/费率/产品包；`pbsdb` 费率策略）

## 业务域速查

### 会员与账户
- 会员主体、认证、密码、设备绑定 → [[tbl_member_db]]
- 实名信息 `member.tm_realname_entity` → [[tbl_member_db]]
- 外部账户余额变动、内部账户明细 → [[tbl_dpm_db]]

### 网关与接入
- 公私钥 `t_key_config`、接口权限 `t_gateway_merchant_api_auth`、接口配置/分组、IP 白名单 → [[tbl_acs_db]]

### 商户与设备
- 商户号 `mid`、门店、员工与角色、账期、定时出款 → [[tbl_merchant_db]]
- 硬件信息、商户绑定设备、激活码、设备申请、设备密钥 → [[tbl_device_db]]

### 交易
- 收单：`acquireii.t_acquire_order` / `t_payment_info` / `t_refund_order`
- 出款服务：`mhtfundout.t_fundout_order` / `t_payment_info` / `t_fundout_account_beneficiary`
- 个人转账：`transfer.t_transfer_order`
- 中台充值/交易/提现：`deposit.t_deposit_order`、`tradeii.t_trade_order` 及扩展/支付订单、`fundout.tt_fundout_order`
- 详见 [[tbl_trade_db]]

### 账单与对账
- 账期、对账单登记/模板/任务/文件、收单对账统计 → [[tbl_statement_db]]

### 费率与定价
- `ppcenter`：产品模板、费率定义、费率配置、产品申请与审核、产品包及与模板关联
- `pbsdb`：费率策略、策略详情、价格计算策略
- 详见 [[tbl_pricing_db]]

### 生活中心
- 订单 `marketorder.t_order`
- 商品 `marketgoods.t_goods_sku`
- 供应商渠道 `supplier.t_supplier_channel`

## 使用建议

- 一笔交易的排查通常按链路：`acs`（接入鉴权）→ `tradeii`/`acquireii`（订单与支付）→ `dpm`（账户变动）→ `statementii`（对账）。
- 商户维度问题先确认 `merchant.t_merchant` 的 `mid` 与 `id`，再关联门店/员工/设备。
- 会员维度优先用 `tm_member_identity` 的 `IDENTITY` 唯一标识贯穿其它会员相关表。

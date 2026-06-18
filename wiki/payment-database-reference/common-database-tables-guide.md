---
title: 常用数据库表速查指南
domain: payment-database-reference
kind: wiki_page
slug: common-database-tables-guide
status: active
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:79d1eee0-a479-47fd-8b3d-ec12172156f3
tags: []
---

# 常用数据库表速查指南

本页按业务域汇总日常排查中最常用的库表及其含义，便于快速定位数据。详细字段说明请进入对应分页。

## 业务域速览

- **会员与账户**：会员、认证、操作员、密码、设备绑定、银行卡、外部/内部账户余额明细 → [[member-database-tables]]
- **网关接入(acs)**：公私钥、接口权限、接口分组、IP 白名单
- **商户与设备**：商户、门店、员工、账期、定时出款、硬件设备、激活码、设备密钥 → [[merchant-device-database-tables]]
- **生活中心**：订单、商品 SKU、供应商渠道
- **账单与交易**：账期登记、对账单模板/任务/文件、收单/退款/出款/转账、中台交易（充值/交易/提现）→ [[trade-statement-database-tables]]
- **费率与策略**：ppcenter 产品模板与费率配置、pbs 费率策略 → [[pricing-database-tables]]

## 会员相关库 (member / dpm)

- `member.tm_member`：会员信息
- `member.tm_member_identity`：会员标识表，保存会员唯一标识 IDENTITY
- `member.tr_verify_entity`：认证实体表，VERIFY_ENTITY_ID 为认证实体 ID
- `member.tr_verify_ref`：认证关系表（1 身份证 / 11 手机 / 12 信箱）
- `member.tr_verify_entity_rel`
- `member.tm_operator`：操作员信息表（密码挂在操作员下）
- `member.tr_password`：会员支付密码信息
- `member.td_config`：配置表
- `member.tr_member_device`：用户设备绑定信息
- `member.tm_device`：设备信息（型号、操作系统等）
- `member.tr_member_account`：会员账户信息
- `member.tr_bank_account`：个人银行卡信息
- `member.tm_realname_entity`：实名信息
- `dpm.t_dpm_outer_account`：会员外部账户信息
- `dpm.t_dpm_outer_account_subset`：外部账户分户表
- `dpm.t_dpm_outer_account_sub_detail`：外部账户分户明细（余额变动）
- `dpm.t_dpm_inner_account_detail`：内部账户余额明细

## 网关接入库 (acs)

- `acs.t_key_config`：公私钥配置
- `acs.t_gateway_merchant_api_auth`：接口权限
- `acs.t_gateway_api_group`：接口配置
- `acs.t_gateway_api_group_relation`：接口分组关系
- `acs.t_reffer_list`：IP 白名单

## 商户库 (merchant)

- `t_merchant`：商户表（mid 商户号、id 商户 ID）
- `t_store`：门店表（merchant_id、id 门店 ID）
- `t_staff` / `t_staff_role`：员工与员工角色
- `t_period`：账期表
- `t_auto_withdraw_registration` / `t_auto_withdraw_order`：定时出款设置与订单

## 设备库 (device)

- `t_hardware_info`：设备信息
- `t_merchant_device`：商户绑定设备
- `t_active_code`：激活码
- `t_device_apply_order`：设备申请列表
- `t_device_key`：设备密钥

## 生活中心类

- `marketorder.t_order`：生活中心订单
- `marketgoods.t_goods_sku`：生活中心商品
- `supplier.t_supplier_channel`：供应商渠道

## 账单库 (statementii)

- `t_statement_period`：账期表
- `t_statement_registration`：对账单登记
- `t_statement_template`：对账单模板
- `t_statement_task`：对账单任务
- `t_statement_file`：对账单文件
- `t_statement_pruchase_statistics`：收单对账单信息统计

## 交易类

- `acquireii.t_acquire_order`：收单交易
- `acquireii.t_payment_info`：收单支付信息
- `acquireii.t_refund_order`：收单退款订单
- `mhtfundout.t_fundout_order`：出款服务订单
- `mhtfundout.t_payment_info`：出款服务支付信息
- `mhtfundout.t_fundout_account_beneficiary`：出款服务收款方信息
- `transfer.t_transfer_order`：个人转账

## 中台交易类

- `deposit.t_deposit_order`：充值
- `tradeii.t_trade_order`：交易
- `tradeii.t_order_ext`：交易订单扩展
- `tradeii.t_payment_order`：交易支付订单
- `fundout.tt_fundout_order`：提现

## 费率配置 (ppcenter)

- `t_product_template`：产品模板
- `t_calculation_define`：费率定义
- `t_price_cal`：费率配置
- `t_product_apply_order`：产品申请
- `t_product_apply_info`：申请审核资料
- `t_package_define`：产品包
- `t_package_template_relation`：产品包与产品模板关联

## 费率策略 (pbsdb)

- `tb_pbs_price_strategy_unit`：费率策略
- `tb_pbs_price_strategy_param`：策略详情
- `tb_pbs_price_cal`：价格计算策略

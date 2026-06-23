---
title: 会员与账户库常用表
domain: payment-database-reference
kind: wiki_page
slug: member-database-tables
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:79d1eee0-a479-47fd-8b3d-ec12172156f3
tags: []
---

# 会员与账户库常用表

本页汇总 `member` 库（会员相关）与 `dpm` 库（会员账户）中常用表，覆盖会员主体、认证、密码、设备绑定、银行卡及内外部账户余额明细。其他库表请参见 [[common-database-tables-guide]]。

## member 库：会员主体与标识

- `tm_member`：会员信息表
- `tm_member_identity`：会员标识表，保存会员唯一标识 `IDENTITY`
- `tm_realname_entity`：实名信息

## 认证相关

- `tr_verify_entity`：认证实体表，每个会员的每种实体认证类型存一条记录，主键 `VERIFY_ENTITY_ID` 为认证实体 ID
- `tr_verify_ref`：认证关系表，记录具体认证类型及其认证实体
  - 类型枚举：`1` 身份证、`11` 手机、`12` 信箱
  - 认证实体即对应的身份证号 / 手机号 / 邮箱
- `tr_verify_entity_rel`

## 操作员与支付密码

- `tm_operator`：操作员信息表，密码挂在操作员下
- `tr_password`：会员支付密码信息表
- `td_config`：配置表

## 设备绑定

- `tr_member_device`：用户设备信息，记录会员绑定的设备 ID 关联
- `tm_device`：设备信息表，存设备型号、操作系统等具体信息

> 商户侧设备见 [[merchant-device-database-tables]]。

## 会员账户与银行卡

- `tr_member_account`：会员账户信息表
- `tr_bank_account`：个人银行卡信息表

## dpm 库：会员账户余额与明细

- `t_dpm_outer_account`：会员外部账户信息
- `t_dpm_outer_account_subset`：外部账户分户表
- `t_dpm_outer_account_sub_detail`：外部账户分户账户明细，记录外部账户余额变动明细
- `t_dpm_inner_account_detail`：内部账户余额明细

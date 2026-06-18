---
id: tbl_member_db
object_type: Table
domain: payment-databases
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:tester/124289264
tags:
- 会员
- 认证
- 密码
- 设备
subdomain: member
module: null
sensitivity: normal
name: 会员相关库(member)核心表
aliases:
- member
related_services: []
related_tables:
- tbl_dpm_db
- tbl_device_db
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
member 库存放会员域核心数据，包括会员基础信息、唯一标识、实名认证、操作员与支付密码、设备绑定、会员账户与银行卡等信息。

## 关键列
- `tm_member`：会员信息表
- `tm_member_identity`：会员标识表，保存会员唯一标识 IDENTITY
- `tr_verify_entity`：认证实体表，每个会员每种实体认证类型存一条记录，`VERIFY_ENTITY_ID` 为认证实体ID
- `tr_verify_ref`：认证关系表，记录认证类型(1身份证 / 11手机 / 12信箱)及其认证实体(身份证号、手机号、邮箱)
- `tr_verify_entity_rel`：认证实体关系表
- `tm_operator`：操作员信息表，密码挂在操作员下
- `tr_password`：会员支付密码信息表
- `td_config`：配置表
- `tr_member_device`：用户设备信息，关联会员绑定的设备ID
- `tm_device`：设备信息表(设备型号、操作系统等)
- `tr_member_account`：会员账户信息表
- `tr_bank_account`：个人银行卡信息表
- `tm_realname_entity`：实名信息

## 主键/索引
原文未提供主键/索引定义。关键关联键：
- `VERIFY_ENTITY_ID`(tr_verify_entity 主键，认证实体ID)
- 会员唯一标识 IDENTITY(tm_member_identity)
- 操作员与 `tr_password` 的归属关系

## 校验点(QA 关注)
- 会员认证排查：通过 `tr_verify_ref` 的认证类型(1身份证/11手机/12信箱)定位 `tr_verify_entity` 中对应实体记录
- 支付密码问题：定位顺序 tm_member → tm_operator → tr_password(密码挂在操作员下)
- 设备绑定核查：`tr_member_device` 与 `tm_device` 关联，确认会员绑定设备及设备型号/操作系统
- 实名校验：`tm_realname_entity` 中实名信息与 `tr_verify_entity`/`tr_verify_ref` 中身份证认证记录一致性
- 会员账户与银行卡：`tr_member_account`、`tr_bank_account` 与会员主键关联完整性

---
id: tbl_merchant_db
object_type: Table
domain: payment-database-reference
status: archived
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:tester/124289264
tags:
- 商户
- 门店
- 员工
- 账期
- 定时出款
subdomain: merchant
module: null
sensitivity: normal
name: 商户库(merchant)核心表
aliases:
- merchant
related_services: []
related_tables:
- tbl_device_db
- tbl_pricing_db
- tbl_statement_db
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
merchant 库存放商户域核心数据，覆盖商户、门店、员工及角色、账期与定时出款等业务对象，是商户身份、组织结构、出款策略相关查询的入口。

## 关键列
- `t_merchant`：商户表
  - `mid`：商户号
  - `id`：商户 id
- `t_store`：门店表
  - `merchant_id`：商户 id
  - `id`：门店 id
- `t_staff`：员工表(门店下员工)
- `t_staff_role`：员工角色表
- `t_period`：账期表
- `t_auto_withdraw_registration`：定时出款设置表
- `t_auto_withdraw_order`：定时出款订单表

## 主键/索引
原文未提供，按表内 `id` / `mid` / `merchant_id` 等字段作为业务主键与关联键使用。

## 校验点(QA 关注)
- 商户层级关系：`t_merchant.id` → `t_store.merchant_id` → `t_staff` 关联是否完整。
- 商户号 `mid` 与商户 id `id` 不要混用：对外业务通常用 `mid`，库内关联用 `id`。
- 员工与角色：`t_staff` 与 `t_staff_role` 的角色挂载是否正确，影响权限。
- 账期 `t_period` 与定时出款：`t_auto_withdraw_registration` 配置是否生效，对应是否生成 `t_auto_withdraw_order` 出款订单。
- 与设备库 [[tbl_device_db]] 的 `t_merchant_device` 关联，确认商户-设备绑定一致；与费率 [[tbl_pricing_db]]、账单 [[tbl_statement_db]] 联动验证。

---
title: WPS数据分布速查
domain: wps-payroll
kind: wiki_page
slug: wps-data-map
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:AQ/2272428082
tags: []
---

# WPS数据分布速查

本页速查 WPS 业务域中各功能区对应的核心数据库表分布，便于排查数据来源与归属。涉及的业务域见 [[domain_wps_payroll]]，整体上下文见 [[wps-knowledge-base-overview]]。

## 公司 (Company)

- `bps.t_corporate`（含 `_profile` / `_account` / `_address` / `_mohre`）
- `vis.t_virtual_account`（IBAN）
- 公司类型差异（SIF / PAF）见 [[wps-sif-vs-paf]]

## 发票 / 计费 (Invoice / Billing)

- `bps.t_corp_invoice_config`
- `bps.t_corp_invoice` / `_item`
- `bps.t_corp_invoice_fee_code` / `_item_code`

## 员工 (Employee)

- 主表（持有状态）：`bps.t_employee_corporate`
- 关联表：`bps.t_employee` / `_profile` / `_salary_account` / `_address`
- 护照 KYC 资料：`bps.t_employee_kyc_material`

## 薪资 (Payroll)

- 通用：
  - `bps.t_payroll_source` / `_bulk` / `_data`
  - `bps.t_salary_load_command` / `_execute`
  - `bps.t_cb001_transfer_record`
  - `bps.t_salary_load_record`
- PAF 专用：
  - `bps.t_payroll_paf` / `_detail`

## 央行文件 (Central-bank files)

- `bps.t_esa_file_record` / `_detail`
- 用于 Non-Listed LRAs 的 EIF / WIF 文件

## 卡片 (Card)

- `ppc.t_virtual_card`：proxy / CVV / 卡状态（YSE 主导，参与方见 [[wps-key-actors]]）
- `bps.t_employee_salary_account`：`card_ref_mid` / `vid`、IBAN、routing
- `bps.t_employee_profile`：`qr_code`

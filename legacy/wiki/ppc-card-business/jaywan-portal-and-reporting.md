---
title: Jaywan门户与报表MIS要求
domain: ppc-card-business
kind: wiki_page
slug: jaywan-portal-and-reporting
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_attachment
source_ref: wiki_attachment:e3c2c891-c5e7-47d3-9cfb-05825c9af14a
tags: []
---

# Jaywan门户与报表MIS要求

本页聚焦Astratech内部门户的运营能力，以及由MBank/Dgpays通过Portal与SFTP共享的报表与MIS清单。门户与报表的数据基础来自[[jaywan-card-integration-scope]]中的卡生命周期与交易流，并与[[jaywan-reconciliation-settlement]]协同使用。

## Portal Requirements (Astratech内部使用)

供Astratech客服与运营团队使用的内部门户，主要能力如下：

- Portal access for Astratech Customer Support and Ops
- Daily Transaction Log View (6 months)
- Card Blocking & Activation
- Chargeback case submission tracking
- Dashboard for card issuance, status, activity
- Daily/Monthly report downloads (Excel/CSV)

## Reporting & MIS

由MBank和/或Dgpays通过Portal和SFTP共享的报表清单：

- Card Issuance Report
- New Cards Report
- Replacements/Reissuance Report
- Card Closure Reports
- Active & Inactive Report
- Merchant Usage Report
- Daily Settlement Report
- Clearing Report
- Authorization Report

## Card Volume 维度指标

报表需按以下维度提供卡量统计：

- Card Type：Virtual / Physical
- Total cards daily & monthly
- Total virtual cards daily & monthly
- Total Physical cards daily & monthly
- Total Active Cards monthly
- Total count of Apple token（若启用）
- Total count of Google token（若启用）

## 关联说明

- 对账文件与结算明细的字段、时效、SFTP交付方式见 [[jaywan-reconciliation-settlement]]。
- 门户中涉及的BIN、产品、限额等配置项见 [[jaywan-product-matrix-and-setup]]。
- 项目背景与整体范围见 [[jaywan-prepaid-card-brd-overview]]。

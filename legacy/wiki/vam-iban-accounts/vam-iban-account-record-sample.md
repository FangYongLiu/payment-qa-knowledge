---
title: VAM IBAN 虚拟账户记录示例
domain: vam-iban
kind: wiki_page
slug: vam-iban-account-record-sample
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_attachment
source_ref: wiki_attachment:f63c9111-f7c9-4f63-8047-ba7096a91d0f
tags: []
---

# VAM IBAN 虚拟账户记录示例

本页展示一条 VAM（Virtual Account Management）虚拟账户的 IBAN 记录样例，用于说明虚拟账户主要字段的取值形态。

## 示例记录

来源：Sheet1，记录键 `40006 — 00000112`。

## 字段明细

| 字段 | 值 |
| --- | --- |
| Virtual Account Entity Identifier | 40006 |
| Virtual Account ID | 00000112 |
| Virtual Account Name | MUHAMMAD TASHFEEN SAEED MALIK MALIK MUHAMMAD SAEED |
| Virtual Account IBAN | AE270357414000620231020 |
| Virtual Account Type | Payment and Collection |
| Hierarchy Type | P |
| Hierarchy Name | 1 |
| Email Address | vamemail@payby.com |
| Contact Number | 0524179822 |
| Address line 1 | United Arab Emirates |
| Address line 2 | DUBAI |
| Address line 3 | AL QOUZ INDUSTRIAL |
| Status | Active |
| Approved / Rejected By | yunzhang |
| Approved / Rejected On | 2022-06-29 13:12:04 |

## 字段说明要点

- **账户标识**：`Virtual Account Entity Identifier` 与 `Virtual Account ID` 共同定位一条虚拟账户记录。
- **IBAN**：`AE270357414000620231020`，符合 UAE IBAN 结构（国家码 `AE` 起始）。
- **账户类型**：`Payment and Collection`，表示同时支持付款与收款。
- **层级信息**：`Hierarchy Type = P`，`Hierarchy Name = 1`。
- **联系信息**：邮箱 `vamemail@payby.com`，联系电话 `0524179822`。
- **地址**：分三行存储，国家、城市、区域分别对应 `Address line 1/2/3`。
- **状态与审批**：`Status = Active`；由 `yunzhang` 于 `2022-06-29 13:12:04` 审批通过。

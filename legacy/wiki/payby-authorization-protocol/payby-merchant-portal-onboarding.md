---
title: PayBy商户控台入驻与信息填写
domain: authorization-protocol
kind: wiki_page
slug: payby-merchant-portal-onboarding
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:18c3aca8-5ff2-457b-ad84-c7800f9db771
tags: []
---

# PayBy商户控台入驻与信息填写

本页说明 PayBy 商户控台（Merchant Portal）入驻流程中关键表单的填写要求，重点覆盖 Company Bank Account（公司银行账户）信息的录入。

## Company Bank Account（公司银行账户）

填写说明：Make sure that the information for both the bank account and the company are the same.（银行账户与公司主体信息须保持一致。）

### 必填字段

表单为两列布局，所有字段均为必填（标记 `*`）：

左列：
- **IBAN** — 输入 IBAN（占位提示 "Enter IBAN"）
- **Account name** — 账户名（占位提示 "Enter Account Name"）
- **City** — 下拉选择城市（"Select City"）

右列：
- **Bank name** — 银行名称（占位提示 "Enter bank name"）
- **Country** — 下拉选择国家，默认值为 `United Arab Emirates`
- **Address** — 地址（占位提示 "Enter Address"），辅助说明："The company address registered in the bank"（即在银行登记的公司地址）

### 无 IBAN 场景

表单底部提供复选框：

- **Company does not have an IBAN** — 默认未勾选；勾选后用于标记公司无 IBAN 的情形（将影响 IBAN 字段的填写要求）。

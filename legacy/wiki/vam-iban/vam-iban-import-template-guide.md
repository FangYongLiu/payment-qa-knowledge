---
title: VAM IBAN虚拟账户导入模板说明
domain: vam-iban
kind: wiki_page
slug: vam-iban-import-template-guide
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki_image
source_ref: wiki_image:b2c542aa-7f1e-491d-b120-ddc51cfd9644
tags: []
---

# VAM IBAN虚拟账户导入模板说明

本页说明 VAM IBAN 虚拟账户导入 Excel 模板的列结构与关键填写规范，用于准备导入文件时参考。

## 模板列结构

模板首行为列头，依次为：

| 列 | 字段 | 示例 |
|----|------|------|
| A | Virtual Account Entity Identifier | 40006 |
| B | Virtual Account ID | 00000112 |
| C | Virtual Account Name | MUHAMMAD TASHFEEN SAEED MALIK MALIK |
| D | Virtual Account IBAN | AE270357414000620231020 |
| E | Virtual Account Type | Payment and Collection |
| F | Hierarchy Type | P |

## 关键字段填写规范

- **Virtual Account ID（B 列）**：对应数据库中的 id。
  - 注意：位数和格式都不要更改，须与库中保持一致。
- **Virtual Account IBAN（D 列）**：修改 IBAN，保证唯一。
  - 建议使用日期方式生成，避免与已有数据重复。

## 其他列说明

- A 列 Virtual Account Entity Identifier、C 列 Virtual Account Name、E 列 Virtual Account Type、F 列 Hierarchy Type 按模板示例数据原样维护。
- 示例中 Virtual Account Type 取值 `Payment and Collection`，Hierarchy Type 取值 `P`。

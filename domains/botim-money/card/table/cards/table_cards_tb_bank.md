---
id: tbl_cards_tb_bank
object_type: Table
name: 银行 (tb_bank)
aliases: [tb_bank, cards.tb_bank]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cards schema DDL
tags: [card, cards]
sensitivity: normal
related_services: []
---

# 银行 (tb_bank)

## 用途
物理表 `cards.tb_bank`,主键 `BANK_CODE`。银行。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `BANK_CODE` | varchar(6) | 银行编码-4/6位 |
| `BANK_NAME` | varchar(128) | 银行名 |
| `BANK_NAME_ALIAS` | varchar(128) | 银行名别名 · 可空 |
| `COUNTRY_CODE` | varchar(2) | 国家编码 |
| `SWIFT_CODE` | varchar(11) | swift编码 |
| `ENTITY_ID` | varchar(3) | 银行编码-数字 |
| `CLEARING_CODE` | varchar(9) | 清算编码 · 可空 |
| `CBID_CODE` | varchar(8) | cbid编码 · 可空 |
| `BANK_PHONE` | varchar(32) | 银行电话 · 可空 |
| `BANK_WEBSITE` | varchar(256) | 银行网站 · 可空 |
| `BANK_LOGO` | varchar(256) | 银行logo · 可空 |
| `ENABLE_FLAG` | char | 启用状态 Y-启用 N-禁用 |
| `MEMO` | varchar(256) | 备注 · 可空 |
| `EXTENSION` | varchar(512) | 扩展参数 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`BANK_CODE`
- `uk_country_bank_name`:BANK_NAME, COUNTRY_CODE (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

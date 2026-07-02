---
id: tbl_cards_tb_card_bin_history
object_type: Table
name: card bin deletion archive (tb_card_bin_history)
aliases: [tb_card_bin_history, cards.tb_card_bin_history]
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

# card bin deletion archive (tb_card_bin_history)

## 用途
物理表 `cards.tb_card_bin_history`,主键 `HISTORY_ID`。card bin deletion archive。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `HISTORY_ID` | bigint | archive primary key · 可空 |
| `ORIGINAL_BIN_ID` | int | snapshot of tb_card_bin.BIN_ID at time of deletion |
| `BANK_CODE` | varchar(32) | issuing bank code copied from tb_card_bin · 可空 |
| `CARD_TYPE` | char(2) | card type: CC=credit DC=debit copied from tb_card_bin · 可空 |
| `CARD_NAME` | varchar(128) | card product name copied from tb_card_bin · 可空 |
| `CARD_BRAND` | varchar(32) | card scheme: VISA MASTERCARD etc copied from tb_card_bin · 可空 |
| `CARD_BIN` | varchar(32) | bank identification number copied from tb_card_bin |
| `CARD_LEN` | decimal(2) | card number length copied from tb_card_bin |
| `CARD_LEVEL` | varchar(32) | card level: CLASSIC PREPAID PLATINUM etc copied from tb_card_bin · 可空 |
| `ENABLE_FLAG` | char | enable flag value at time of deletion copied from tb_card_bin · 可空 |
| `SOURCE_VERSION` | varchar(64) | tb_card_bin.VERSION value at moment of deletion · 可空 |
| `MANUAL_FLAG` | char | manual entry flag copied from tb_card_bin · 可空 |
| `MEMO` | varchar(256) | bank name for foreign cards copied from tb_card_bin · 可空 |
| `EXTENSION` | varchar(512) | extended data copied from tb_card_bin · 可空 |
| `SOURCE_GMT_CREATE` | timestamp | original row create time from tb_card_bin.GMT_CREATE · 可空 |
| `SOURCE_GMT_MODIFIED` | timestamp | original row last modified time from tb_card_bin.GMT_MODIFIED · 可空 |
| `DELETE_VERSION` | varchar(64) | import batch version that triggered the deletion |
| `DELETE_FILE_ID` | int | import_file.fileId that triggered the deletion |
| `DELETE_OPERATOR` | varchar(64) | operator username who triggered the import deletion · 可空 |
| `DELETE_TIME` | timestamp | timestamp when this archive record was created |
| `GMT_CREATE` | timestamp | archive table row create time |

## 主键 / 索引
- 主键:`HISTORY_ID`
- `idx_card_bin_len`:CARD_BIN, CARD_LEN
- `idx_delete_file_id`:DELETE_FILE_ID
- `idx_delete_version`:DELETE_VERSION

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

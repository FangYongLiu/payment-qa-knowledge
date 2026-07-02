---
id: tbl_cards_tb_card_bin
object_type: Table
name: 卡bin (tb_card_bin)
aliases: [tb_card_bin, cards.tb_card_bin]
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

# 卡bin (tb_card_bin)

## 用途
物理表 `cards.tb_card_bin`,主键 `BIN_ID`。卡bin。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `BIN_ID` | int(15) | 卡bin主键 · 可空 |
| `BANK_CODE` | varchar(6) | 银行编码 |
| `CARD_TYPE` | char(2) | 卡类型 CC-信用卡,DC-借记卡 |
| `CARD_NAME` | varchar(64) | 卡名 · 可空 |
| `CARD_BRAND` | varchar(10) | 卡品牌 · 可空 |
| `CARD_BIN` | varchar(11) | 卡bin |
| `CARD_LEN` | int(2) | 卡号长度 |
| `CARD_LEVEL` | varchar(32) | 卡等级 · 可空 |
| `ENABLE_FLAG` | char | 启用状态 |
| `MANUAL_FLAG` | char | 是否人工修改数据 · 可空 |
| `VERSION` | varchar(16) | 版本号 · 可空 |
| `MEMO` | varchar(256) | 备注 · 可空 |
| `EXTENSION` | varchar(512) | 扩展参数 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`BIN_ID`
- `uk_card_bin_len`:CARD_BIN, CARD_LEN (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

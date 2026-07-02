---
id: tbl_cards_tb_state
object_type: Table
name: 邦 (tb_state)
aliases: [tb_state, cards.tb_state]
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

# 邦 (tb_state)

## 用途
物理表 `cards.tb_state`,主键 `STATE_ID`。邦。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `STATE_ID` | bigint(15) | 邦Id |
| `STATE_NAME` | varchar(128) | 邦全称 |
| `STATE_CODE` | varchar(3) | 邦编码 · 可空 |
| `COUNTRY_CODE` | varchar(2) | 国家编码 |
| `STATE_SHORTNAME` | varchar(128) | 邦简称 · 可空 |
| `STATE_ARABIC` | varchar(256) | 邦阿拉伯名 · 可空 |
| `ENABLE_FLAG` | char | 启用标识 |
| `MEMO` | varchar(256) | 备注 · 可空 |
| `VERSION` | varchar(16) | 版本 |
| `EXTENSION` | varchar(512) | 扩展信息 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`STATE_ID`
- `UK_PROVINFO_PROVNAME`:STATE_NAME (UNIQUE)
- `UK_PROVINFO_PROVSHORTNAME`:STATE_SHORTNAME

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

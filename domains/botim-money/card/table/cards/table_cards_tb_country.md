---
id: tbl_cards_tb_country
object_type: Table
name: 国家 (tb_country)
aliases: [tb_country, cards.tb_country]
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

# 国家 (tb_country)

## 用途
物理表 `cards.tb_country`,主键 `COUNTRY_CODE`。国家。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `COUNTRY_CODE` | char(2) | 国家代码 |
| `COUNTRY_NAME` | varchar(128) | 国家名 |
| `CC3` | char(3) | 国家代码-3位 |
| `ALIAS` | varchar(128) | 备注 · 可空 |
| `ENABLE_FLAG` | char | 是否启用, Y-启用, N-禁用 |
| `MEMO` | varchar(256) | 备注 · 可空 |
| `EXTENSION` | varchar(512) | 扩展参数 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`COUNTRY_CODE`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

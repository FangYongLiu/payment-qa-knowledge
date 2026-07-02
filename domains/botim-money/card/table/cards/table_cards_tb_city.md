---
id: tbl_cards_tb_city
object_type: Table
name: 城市 (tb_city)
aliases: [tb_city, cards.tb_city]
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

# 城市 (tb_city)

## 用途
物理表 `cards.tb_city`,主键 `CITY_ID`。城市。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `CITY_ID` | bigint(15) | 城市Id |
| `STATE_ID` | bigint(15) | 所属省份Id |
| `CITY_NAME` | varchar(128) | 城市全称 |
| `CITY_SHORTNAME` | varchar(128) | 城市简称 · 可空 |
| `CITY_ARABIC` | varchar(256) | 城市阿拉伯名 · 可空 |
| `EXTENSION` | varchar(512) | 扩展信息 · 可空 |
| `ENABLE_FLAG` | char | 启用标识 |
| `MEMO` | varchar(256) | 备注 · 可空 |
| `VERSION` | varchar(16) | 版本 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`CITY_ID`
- `UK_CITYINFO_PROVID_CITYNAME`:STATE_ID, CITY_NAME (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_cards_tb_area
object_type: Table
name: 地区 (tb_area)
aliases: [tb_area, cards.tb_area]
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

# 地区 (tb_area)

## 用途
物理表 `cards.tb_area`,主键 `AREA_ID`。地区。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `AREA_ID` | bigint(15) | 地区ID |
| `AREA_NAME` | varchar(128) | 地区全称 |
| `AREA_SHORTNAME` | varchar(128) | 地区简称 · 可空 |
| `AREA_ARABIC` | varchar(256) | 地区阿拉伯语 · 可空 |
| `STATE_ID` | bigint(15) | 所属省份Id |
| `CITY_ID` | bigint(15) | 所属城市Id |
| `ENABLE_FLAG` | char | 启用标识：Y=启用，N=停用 |
| `MEMO` | varchar(256) | 备注 · 可空 |
| `VERSION` | varchar(16) | 版本 |
| `EXTENSION` | varchar(512) | 扩展信息 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`AREA_ID`
- `I_AREAINFO_VERSION`:VERSION

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

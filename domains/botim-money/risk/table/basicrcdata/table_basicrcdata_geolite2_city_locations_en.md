---
id: tbl_basicrcdata_geolite2_city_locations_en
object_type: Table
name: geolite2_city_locations_en (geolite2_city_locations_en)
aliases: [geolite2_city_locations_en, basicrcdata.geolite2_city_locations_en]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: basicrcdata schema DDL
tags: [risk, basicrcdata]
sensitivity: normal
related_services: []
---

# geolite2_city_locations_en (geolite2_city_locations_en)

## 用途
物理表 `basicrcdata.geolite2_city_locations_en`,主键 `geoname_id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `geoname_id` | int(10) | 地理位置id |
| `locale_code` | varchar(64) | 地区代码 · 可空 |
| `continent_code` | varchar(64) | 大陆代码 · 可空 |
| `continent_name` | varchar(64) | 大陆名称 · 可空 |
| `country_iso_code` | varchar(64) | 国家代码 · 可空 |
| `country_name` | varchar(255) | 国家名称 · 可空 |
| `subdivision_1_iso_code` | varchar(64) | 国家一级地区（类似省）code · 可空 |
| `subdivision_1_name` | varchar(255) | 国家一级地区（类似省）名称 · 可空 |
| `subdivision_2_iso_code` | varchar(64) | 国家二级地区（类似市）code · 可空 |
| `subdivision_2_name` | varchar(255) | 国家二级地区名称 · 可空 |
| `city_name` | varchar(255) | 城市名称 · 可空 |
| `metro_code` | varchar(64) | 地铁号 · 可空 |
| `time_zone` | varchar(64) | 时区 · 可空 |
| `is_in_european_union` | tinyint | 是否在欧盟 · 可空 |

## 主键 / 索引
- 主键:`geoname_id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

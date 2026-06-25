---
id: tbl_aml_t_geolite2_city_locations_en
object_type: Table
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (aml schema) 2026-06-25
tags:
- aml
- aml
- t_geolite2_city_locations_en
subdomain: aml
module: null
sensitivity: normal
name: GeoLite2 城市位置(t_geolite2_city_locations_en)
aliases:
- t_geolite2_city_locations_en
related_services:
- svc_aml
related_scenarios: []
---
# GeoLite2 城市位置(t_geolite2_city_locations_en)

## 用途
GeoLite2 城市位置。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `geoname_id` | int | PK / NOT NULL | 地理位置id |
| `locale_code` | varchar(64) |  | 地区代码 |
| `continent_code` | varchar(64) |  | 大陆代码 |
| `continent_name` | varchar(64) |  | 大陆名称 |
| `country_iso_code` | varchar(64) |  | 国家代码 |
| `country_name` | varchar(255) |  | 国家名称 |
| `subdivision_1_iso_code` | varchar(64) |  | 国家一级地区（类似省）code |
| `subdivision_1_name` | varchar(255) |  | 国家一级地区（类似省）名称 |
| `subdivision_2_iso_code` | varchar(64) |  | 国家二级地区（类似市）code |
| `subdivision_2_name` | varchar(255) |  | 国家二级地区名称 |
| `city_name` | varchar(255) |  | 城市名称 |
| `metro_code` | varchar(64) |  | 地铁号 |
| `time_zone` | varchar(64) |  | 时区 |
| `is_in_european_union` | tinyint |  | 是否在欧盟 |

## 主键 / 索引
- 主键:(`geoname_id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

---
id: tbl_aml_t_geolite2_city_blocks_ipv4
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
- t_geolite2_city_blocks_ipv4
subdomain: aml
module: null
sensitivity: normal
name: GeoLite2 城市IPv4网段(t_geolite2_city_blocks_ipv4)
aliases:
- t_geolite2_city_blocks_ipv4
related_services:
- svc_aml
related_scenarios: []
---
# GeoLite2 城市IPv4网段(t_geolite2_city_blocks_ipv4)

## 用途
GeoLite2 城市IPv4网段。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC |  |
| `ip_from` | int |  | 子网开始ip |
| `ip_to` | int |  | 子网结束ip |
| `network` | varchar(255) |  | 子网表示字符串 |
| `geoname_id` | int |  | ip所在地地理名称id |
| `registered_country_geoname_id` | int |  | 注册国家所在地地理名称id |
| `represented_country_geoname_id` | int |  | 代表国家所在地地理名称id |
| `is_anonymous_proxy` | tinyint |  | 是否是匿名代理ip |
| `is_satellite_provider` | tinyint |  | 是否是卫星电视提供商ip |
| `postal_code` | int |  | 邮编 |
| `latitude` | int |  | 维度 |
| `longitude` | int |  | 经度 |
| `accuracy_radius` | int |  | 经度维度范围半径 |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `ip_f_to_inx` 唯一 (ip_from, ip_to)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

---
id: tbl_basicrcdata_t_geolite2_ipinfo_v2
object_type: Table
name: t_geolite2_ipinfo_v2 (t_geolite2_ipinfo_v2)
aliases: [t_geolite2_ipinfo_v2, basicrcdata.t_geolite2_ipinfo_v2]
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

# t_geolite2_ipinfo_v2 (t_geolite2_ipinfo_v2)

## 用途
物理表 `basicrcdata.t_geolite2_ipinfo_v2`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | id · 可空 |
| `ip_from` | int unsigned | 子网开始ip · 可空 |
| `ip_to` | int unsigned | 子网结束ip · 可空 |
| `network` | varchar(255) | 子网表示字符串 · 可空 |
| `geoname_id` | int(10) | ip所在地地理名称id · 可空 |
| `registered_country_geoname_id` | int(10) | 注册国家所在地地理名称id · 可空 |
| `represented_country_geoname_id` | int(10) | 代表国家所在地地理名称id · 可空 |
| `is_anonymous_proxy` | tinyint | 是否是匿名代理ip · 可空 |
| `is_satellite_provider` | tinyint | 是否是卫星电视提供商ip · 可空 |
| `postal_code` | int(10) | 邮编 · 可空 |
| `latitude` | double | 纬度 · 可空 |
| `longitude` | double | 经度 · 可空 |
| `accuracy_radius` | int(10) | 经度维度范围半径 · 可空 |

## 主键 / 索引
- 主键:`id`
- `ip_f_to_inx`:ip_from, ip_to (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

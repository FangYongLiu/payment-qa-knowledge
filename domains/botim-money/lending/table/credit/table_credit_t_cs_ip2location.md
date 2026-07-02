---
id: tbl_credit_t_cs_ip2location
object_type: Table
name: t_cs_ip2location (t_cs_ip2location)
aliases: [t_cs_ip2location, credit.t_cs_ip2location]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: credit schema DDL
tags: [lending, credit]
sensitivity: normal
related_services: []
---

# t_cs_ip2location (t_cs_ip2location)

## 用途
物理表 `credit.t_cs_ip2location`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `ip_from` | int unsigned | 子网开始ip · 可空 |
| `ip_to` | int unsigned | 子网结束ip · 可空 |
| `country_code` | char(2) | 国家英文缩写 · 可空 |
| `country_name` | varchar(64) | 国家名称 · 可空 |
| `region_name` | varchar(128) | 地区名称 · 可空 |
| `city_name` | varchar(128) | 城市名称 · 可空 |
| `latitude` | double | 纬度 · 可空 |
| `longitude` | double | 经度 · 可空 |
| `zip_code` | varchar(30) | 邮编 · 可空 |
| `time_zone` | varchar(8) | 时区 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_ip_from_to`:ip_from, ip_to (UNIQUE)
- `idx_ip_to`:ip_to (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

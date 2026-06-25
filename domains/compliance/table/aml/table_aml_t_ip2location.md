---
id: tbl_aml_t_ip2location
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
- t_ip2location
subdomain: aml
module: null
sensitivity: normal
name: IP地理位置库(t_ip2location)
aliases:
- t_ip2location
related_services:
- svc_aml
related_scenarios: []
---
# IP地理位置库(t_ip2location)

## 用途
IP地理位置库。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC |  |
| `ip_from` | int |  | 子网开始ip |
| `ip_to` | int |  | 子网结束ip |
| `country_code` | char(2) |  | 国家英文缩写 |
| `country_name` | varchar(64) |  | 国家名称 |
| `region_name` | varchar(128) |  | 地区名称 |
| `city_name` | varchar(128) |  | 城市名称 |
| `latitude` | double |  | 纬度 |
| `longitude` | double |  | 经度 |
| `zip_code` | varchar(30) |  | 邮编 |
| `time_zone` | varchar(8) |  | 时区 |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `idx_ip_from_to` 唯一 (ip_from, ip_to)
  - `idx_ip_to` 唯一 (ip_to)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

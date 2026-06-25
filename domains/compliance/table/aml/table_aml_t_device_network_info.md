---
id: tbl_aml_t_device_network_info
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
- t_device_network_info
subdomain: aml
module: null
sensitivity: normal
name: 设备网络信息表(t_device_network_info)
aliases:
- t_device_network_info
related_services:
- svc_aml
related_scenarios: []
---
# 设备网络信息表(t_device_network_info)

## 用途
设备网络信息表。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键 |
| `session_id` | varchar(64) | NOT NULL | session id |
| `dns_ip` | varchar(16) |  | dbs ip |
| `dns_ip_city` | varchar(256) |  | DNS IP所在的城市 |
| `dns_ip_geo` | varchar(4) |  | DNS IP地址的2个字符的ISO 2国家/地区代码 |
| `dns_ip_isp` | varchar(64) |  | DNS IP地址来源的ISP |
| `dns_ip_latitude` | varchar(20) |  | DNS IP的纬度 |
| `dns_ip_longitude` | varchar(20) |  | DNS IP的经度 |
| `dns_ip_organization` | varchar(64) |  | DNS IP地址的来源组织 |
| `proxy_ip` | varchar(16) |  | 代理ip |
| `proxy_ip_city` | varchar(64) |  | 代理ip的城市 |
| `proxy_ip_geo` | varchar(4) |  | 代理ip地址的2个字符的ISO 2国家/地区代码 |
| `proxy_ip_latitude` | varchar(20) |  | 代理IP的维度 |
| `proxy_ip_longitude` | varchar(20) |  | 代理IP的经度 |
| `proxy_ip_organization` | varchar(64) |  | 代理IP地址的来源组织 |
| `true_ip` | varchar(16) |  | 真实IP |
| `true_ip_city` | varchar(64) |  | 真实IP城市 |
| `true_ip_geo` | varchar(4) |  | 真实IP地址的2个字符的ISO 2国家/地区代码 |
| `true_ip_isp` | varchar(64) |  | 真实IP地址来源的ISP |
| `true_ip_latitude` | varchar(20) |  | 真实IP维度 |
| `true_ip_longitude` | varchar(20) |  | 真实IP经度 |
| `true_ip_organization` | varchar(64) |  | 真实IP地址的来源组织 |
| `local_ipv4` | varchar(128) |  | 本地IPV4地址 |
| `local_ipv6` | varchar(256) |  | 本地IPV6地址 |
| `vm_index` | varchar(6) |  | 是否虚拟机(分值越高越可能) |
| `vm_reason` | varchar(256) |  | 是vm理由 |
| `vpn_score` | varchar(8) |  | 使用vpn分值 |
| `vpn_reason` | varchar(256) |  | 使用vpn理由 |
| `create_time` | timestamp | 默认 CURRENT_TIMESTAMP | 创建时间 |
| `update_time` | timestamp | 默认 CURRENT_TIMESTAMP | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `create_time_session_id` (create_time, session_id)
  - `session_id` (session_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

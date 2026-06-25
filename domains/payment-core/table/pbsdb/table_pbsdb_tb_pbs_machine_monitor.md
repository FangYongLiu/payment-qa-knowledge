---
id: tbl_pbsdb_tb_pbs_machine_monitor
object_type: Table
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (pbsdb schema) 2026-06-25
tags:
- pbsdb
- pricing
- tb_pbs_machine_monitor
subdomain: pricing
module: null
sensitivity: normal
name: 机器监控(tb_pbs_machine_monitor)
aliases:
- tb_pbs_machine_monitor
related_services:
- svc_pbs
related_scenarios: []
---
# 机器监控(tb_pbs_machine_monitor)

## 用途
机器监控。属 pbsdb 库,由 [[svc_pbs]] 读写。

## 关联关系
- **所属服务**:[[svc_pbs]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `UUID` | varchar(32) | PK / NOT NULL | UUID |
| `MACHINE_IP` | varchar(15) |  | 机器IP |
| `MACHINE_NAME` | varchar(500) |  | 机器名称 |
| `CACHE_SIZE` | decimal(15) |  | 缓存大小 |
| `HIT_COUNT` | decimal(15) |  | 命中数 |
| `MISS_COUNT` | decimal(15) |  | 未命中数 |
| `FORCE_REFRESH` | char |  | 强制刷新 |
| `CACHE_UPDATED_TIME` | timestamp |  | 刷新时间 |
| `CACHE_MINUTES` | decimal(15) |  | 缓存时间 |
| `CREATE_TIME` | timestamp | NOT NULL | 创建时间 |
| `MODIFY_TIME` | timestamp |  | 修改时间 |
| `CACHE_MAX_SIZE` | decimal(15) |  | 缓存大小 |
| `TOTAL_MEM` | decimal(15) |  | 总 |
| `FREE_MEM` | decimal(15) |  | 空闲 |
| `MAX_MEM` | decimal(15) |  | 最大 |

## 主键 / 索引
- 主键:(`UUID`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

---
id: tbl_pbsdb_tb_pbs_cachae_log
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
- tb_pbs_cachae_log
subdomain: pricing
module: null
sensitivity: normal
name: 缓存使用日志(tb_pbs_cachae_log)
aliases:
- tb_pbs_cachae_log
related_services:
- svc_pbs
related_scenarios: []
---
# 缓存使用日志(tb_pbs_cachae_log)

## 用途
缓存使用日志。属 pbsdb 库,由 [[svc_pbs]] 读写。

## 关联关系
- **所属服务**:[[svc_pbs]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `CACHAE_LOG_ID` | decimal(15) | PK / NOT NULL | 缓存使用日志ID |
| `GMT_START` | timestamp | NOT NULL | 统计开始时间 |
| `GMT_END` | timestamp |  | 统计结束时间 |
| `CACHE_TYPE` | varchar(2) |  | 缓存类型 |
| `COUNT_ALL` | decimal(11) |  | 总数 |
| `COUNT_MATCH` | decimal(11) |  | 命中数量 |
| `GMT_MODIFIED` | timestamp |  | 最后更新时间 |

## 主键 / 索引
- 主键:(`CACHAE_LOG_ID`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

---
id: tbl_acs_t_rate_limit_config
object_type: Table
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (acs schema) 2026-06-25
tags:
- acs
- acs
- t_rate_limit_config
subdomain: acs
module: null
sensitivity: normal
name: 限流配置，配置表，1000行(t_rate_limit_config)
aliases:
- t_rate_limit_config
related_services:
- svc_acs
related_scenarios: []
---
# 限流配置，配置表，1000行(t_rate_limit_config)

## 用途
限流配置，配置表，1000行。属 acs 库,由 [[svc_acs]] 读写。

## 关联关系
- **所属服务**:[[svc_acs]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `RATE_LIMIT_GROUP` | varchar(30) | PK / NOT NULL | 限流分组 |
| `GROUP_NAME` | varchar(50) | NOT NULL | 分组名称 |
| `GLOBAL_RULE` | varchar(100) | NOT NULL | 全局规则 |
| `MERCHANT_RULE` | varchar(100) | NOT NULL | 商户规则 |
| `EXTENSION` | varchar(2000) |  | 扩展信息 |
| `GMT_CREATE` | timestamp | NOT NULL | 创建时间 |
| `GMT_MODIFY` | timestamp | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`RATE_LIMIT_GROUP`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

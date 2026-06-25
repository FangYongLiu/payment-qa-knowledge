---
id: tbl_tradeii_leaf_alloc
object_type: Table
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (tradeii schema) 2026-06-25
tags:
- tradeii
- infra
- leaf_alloc
subdomain: infra
module: null
sensitivity: normal
name: 序列分配(leaf_alloc)
aliases:
- leaf_alloc
related_services:
- svc_tradeii
related_scenarios: []
---
# 序列分配(leaf_alloc)

## 用途
待补。属 tradeii 库(交易/支付/退款核心),由 [[svc_tradeii]] 读写。

## 关联关系
- **所属服务**:[[svc_tradeii]](交易核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `biz_tag` | varchar(128) | PK / NOT NULL / 默认 '' | sequence名称 |
| `max_id` | bigint | NOT NULL / 默认 1 | 当前序列最大值 |
| `step` | int | NOT NULL | 缓存的个数，一般配置表为10，订单表为200以上，看订单量 |
| `description` | varchar(256) |  | 描述 |
| `update_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 更新时间 |

## 主键 / 索引
- 主键:(`biz_tag`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

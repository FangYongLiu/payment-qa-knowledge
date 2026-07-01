---
id: tbl_pbsdb_leaf_alloc
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
- leaf_alloc
subdomain: pricing
module: null
sensitivity: normal
name: 序列分配(leaf_alloc)
aliases:
- leaf_alloc
related_services:
- svc_pbs
related_scenarios: []
---
# 序列分配(leaf_alloc)

## 用途
序列分配。属 pbsdb 库,由 [[svc_pbs]] 读写。

## 关联关系
- **所属服务**:[[svc_pbs]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `biz_tag` | varchar(128) | PK / NOT NULL / 默认 '' | sequence名称 |
| `max_id` | bigint | NOT NULL / 默认 1 | 当前序列最大值，亦即下次取值的初始值 |
| `step` | int | NOT NULL | 初始情况下在内存中缓冲的序列号个数，一般配置表为10，订单表为200以上，看订单量 |
| `description` | varchar(256) |  | 描述 |
| `update_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 更新时间 |

## 主键 / 索引
- 主键:(`biz_tag`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

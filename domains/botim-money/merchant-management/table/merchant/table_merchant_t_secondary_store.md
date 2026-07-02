---
id: tbl_merchant_t_secondary_store
object_type: Table
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (merchant schema) 2026-06-25
tags:
- merchant
- merchant
- t_secondary_store
subdomain: merchant
module: null
sensitivity: normal
name: 二级门店(t_secondary_store)
aliases:
- t_secondary_store
related_services:
- svc_merchant
related_scenarios: []
---
# 二级门店(t_secondary_store)

## 用途
二级门店。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | 主键 |
| `secondary_merchant_id` | bigint | NOT NULL | 二级商户id |
| `secondary_store_no` | varchar(64) | NOT NULL | 二级门店编号 |
| `merchant_mid` | varchar(50) | NOT NULL | 商户mid |
| `name` | varchar(256) | NOT NULL | 门店名称 |
| `address` | varchar(500) | NOT NULL | 门店地址 |
| `status` | varchar(20) | NOT NULL | 状态, ENABLED 可用; INVALID 失效 |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `last_updated_time` | timestamp | NOT NULL | 最后更新时间 |
| `data_version` | bigint | NOT NULL | 数据版本 |
| `source` | varchar(64) |  | 来源 |
| `creator` | varchar(128) |  | 创建者 |
| `store_id` | bigint |  | 一级门店Id |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uid_store_no` 唯一 (secondary_merchant_id, secondary_store_no, merchant_mid)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

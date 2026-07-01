---
id: tbl_merchant_t_merchant_biz_open
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
- t_merchant_biz_open
subdomain: merchant
module: null
sensitivity: normal
name: 商户业务开通表(t_merchant_biz_open)
aliases:
- t_merchant_biz_open
related_services:
- svc_merchant
related_scenarios: []
---
# 商户业务开通表(t_merchant_biz_open)

## 用途
商户业务开通表。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | id |
| `merchant_creation_id` | bigint | NOT NULL | 商户创建id |
| `merchant_mid` | varchar(50) |  | 商户id |
| `biz_type` | varchar(32) | NOT NULL | 业务类型 |
| `params` | varchar(1000) |  | 参数，json存储 |
| `apply_mid` | varchar(32) | NOT NULL | 申请人 |
| `approver` | varchar(32) |  | 复核人 |
| `created_time` | timestamp | NOT NULL | 创建时间 |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `UK_BIZ` 唯一 (merchant_mid, biz_type)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

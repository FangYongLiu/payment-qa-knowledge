---
id: tbl_merchant_t_common_batch_detail_content_param
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
- t_common_batch_detail_content_param
subdomain: merchant
module: null
sensitivity: normal
name: 批次明细扩展表(t_common_batch_detail_content_param)
aliases:
- t_common_batch_detail_content_param
related_services:
- svc_merchant
related_scenarios: []
---
# 批次明细扩展表(t_common_batch_detail_content_param)

## 用途
批次明细扩展表。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `detail_id` | bigint | PK / NOT NULL | 明细ID |
| `pkey` | varchar(200) | PK / NOT NULL | 参数键 |
| `value` | varchar(500) | NOT NULL | 参数值 |

## 主键 / 索引
- 主键:(`detail_id`, `pkey`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

---
id: tbl_merchant_t_common_batch_detail
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
- t_common_batch_detail
subdomain: merchant
module: null
sensitivity: normal
name: 批次明细(t_common_batch_detail)
aliases:
- t_common_batch_detail
related_services:
- svc_merchant
related_scenarios: []
---
# 批次明细(t_common_batch_detail)

## 用途
批次明细。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | 主键 |
| `batch_id` | bigint | NOT NULL | 批次id |
| `merchant_mid` | varchar(50) | NOT NULL | 商户mid |
| `detail_no` | varchar(64) | NOT NULL | 明细编号 |
| `status` | varchar(32) | NOT NULL | 状态 CREATED 已创建; SUCCESS 成功 ; FAIL 失败 |
| `error_code` | varchar(50) |  | 错误码 |
| `error_message` | varchar(500) |  | 错误信息 |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `last_updated_time` | timestamp | NOT NULL | 最后更新时间 |
| `data_version` | bigint | NOT NULL | 数据版本 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_batchid_status` (batch_id, status)
  - `idx_detail_no` (detail_no)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

---
id: tbl_merchant_t_common_batch
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
- t_common_batch
subdomain: merchant
module: null
sensitivity: normal
name: 公共批次(t_common_batch)
aliases:
- t_common_batch
related_services:
- svc_merchant
related_scenarios: []
---
# 公共批次(t_common_batch)

## 用途
公共批次。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | 主键 |
| `batch_no` | varchar(50) | NOT NULL | 批次编号 |
| `merchant_mid` | varchar(50) | NOT NULL | 商户mid |
| `business_type` | varchar(100) | NOT NULL | 业务类型 SECONDARY_MERCHANT_ON_BOARDING |
| `file_path` | varchar(200) | NOT NULL | 文件路径 |
| `status` | varchar(32) | NOT NULL | 状态  CREATED 已创建; PROCESSING 处理中; FINISHED 已完成 |
| `total_records` | int | NOT NULL | 总记录数 |
| `success_records` | int |  | 成功数 |
| `fail_records` | int |  | 失败数 |
| `error_code` | varchar(50) |  | 错误码 |
| `error_message` | varchar(500) |  | 错误信息 |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `last_updated_time` | timestamp | NOT NULL | 最后更新时间 |
| `data_version` | bigint | NOT NULL | 数据版本 |
| `source` | varchar(64) |  | 来源 |
| `creator` | varchar(128) |  | 创建者 |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uid_batch_no` 唯一 (batch_no)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

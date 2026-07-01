---
id: tbl_merchant_t_pay_type
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
- t_pay_type
subdomain: merchant
module: null
sensitivity: normal
name: 全局支付渠道配置(t_pay_type)
aliases:
- t_pay_type
related_services:
- svc_merchant
related_scenarios: []
---
# 全局支付渠道配置(t_pay_type)

## 用途
全局支付渠道配置。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | id |
| `name` | varchar(32) | NOT NULL | 名称 |
| `code` | varchar(32) | NOT NULL | 编码 |
| `direct_code` | varchar(100) | NOT NULL | direct code |
| `logo_url` | varchar(255) |  | 图标 |
| `description` | varchar(200) |  | 描述 |
| `status` | varchar(32) | NOT NULL | 状态 |
| `pay_rank` | int(3) |  | 排序 |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `last_updated_time` | timestamp | NOT NULL | 最后更新时间 |
| `data_version` | bigint | NOT NULL | 数据版本 |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `UID_CODE` 唯一 (code)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

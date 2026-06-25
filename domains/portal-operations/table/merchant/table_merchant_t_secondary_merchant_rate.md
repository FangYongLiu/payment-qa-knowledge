---
id: tbl_merchant_t_secondary_merchant_rate
object_type: Table
domain: portal-operations
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (merchant schema) 2026-06-25
tags:
- merchant
- merchant
- t_secondary_merchant_rate
subdomain: merchant
module: null
sensitivity: normal
name: 二级商户费率(t_secondary_merchant_rate)
aliases:
- t_secondary_merchant_rate
related_services:
- svc_merchant
related_scenarios: []
---
# 二级商户费率(t_secondary_merchant_rate)

## 用途
二级商户费率。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | 主键 |
| `merchant_mid` | varchar(50) | NOT NULL | 商户mid |
| `secondary_merchant_no` | varchar(64) | NOT NULL | 二级商户编号 |
| `rate` | decimal(8,6) | NOT NULL | 费率 |
| `vat` | decimal(8,6) | NOT NULL | vat |
| `rebate` | decimal(8,6) | NOT NULL | 抽佣比例 |
| `status` | varchar(32) | NOT NULL | 状态  SUBMITTED 已提交， DEPLOYED 已部署， EDITED 已编辑 |
| `creator` | varchar(200) | NOT NULL | 创建者 |
| `source` | varchar(64) | NOT NULL | 来源 |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `last_updated_time` | timestamp | NOT NULL | 最后更新时间 |
| `data_version` | bigint | NOT NULL | 数据版本 |
| `product_pkg_code` | varchar(50) |  | 产品包代码 |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_second_mid` 唯一 (secondary_merchant_no, merchant_mid)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

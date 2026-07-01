---
id: tbl_merchant_t_secondary_merchant
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
- t_secondary_merchant
subdomain: merchant
module: null
sensitivity: normal
name: 二级商户(t_secondary_merchant)
aliases:
- t_secondary_merchant
related_services:
- svc_merchant
related_scenarios: []
---
# 二级商户(t_secondary_merchant)

## 用途
二级商户。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | 主键 |
| `secondary_merchant_no` | varchar(64) | NOT NULL | 二级商户编号 |
| `merchant_mid` | varchar(50) | NOT NULL | 商户mid |
| `name` | varchar(256) | NOT NULL | 名称 |
| `register_country` | varchar(20) | NOT NULL | 注册国家 |
| `industry` | varchar(20) | NOT NULL | 行业  4位MCC代码 |
| `status` | varchar(20) | NOT NULL | 状态, ENABLED 可用; INVALID 失效 |
| `contact_name` | varchar(256) |  | 联系人 |
| `contact_mobile` | varchar(64) |  | 联系电话 |
| `contact_email` | varchar(128) |  | 联系邮箱 |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `last_updated_time` | timestamp | NOT NULL | 最后更新时间 |
| `data_version` | bigint | NOT NULL | 数据版本 |
| `source` | varchar(64) |  | 来源 |
| `creator` | varchar(128) |  | 创建者 |
| `rate_id` | bigint |  | 费率id |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uid_merchant_no` 唯一 (secondary_merchant_no, merchant_mid)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

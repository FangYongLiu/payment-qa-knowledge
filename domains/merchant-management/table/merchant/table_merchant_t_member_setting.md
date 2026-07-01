---
id: tbl_merchant_t_member_setting
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
- t_member_setting
subdomain: merchant
module: null
sensitivity: normal
name: 会员配置(t_member_setting)
aliases:
- t_member_setting
related_services:
- svc_merchant
related_scenarios: []
---
# 会员配置(t_member_setting)

## 用途
会员配置。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | 主键 |
| `member_id` | varchar(50) | NOT NULL | 会员id |
| `config_key` | varchar(50) | NOT NULL | 配置键 |
| `config_value` | varchar(1000) | NOT NULL | 配置值 |
| `memo` | varchar(255) |  | 备注说明 |
| `created_time` | timestamp | NOT NULL | 创建时间 |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_mid_key` 唯一 (member_id, config_key)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

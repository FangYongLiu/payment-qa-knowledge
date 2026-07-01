---
id: tbl_merchant_t_member_2fa_config
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
- t_member_2fa_config
subdomain: merchant
module: null
sensitivity: normal
name: 会员2FA配置(t_member_2fa_config)
aliases:
- t_member_2fa_config
related_services:
- svc_merchant
related_scenarios: []
---
# 会员2FA配置(t_member_2fa_config)

## 用途
会员2FA配置。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | id |
| `mid` | varchar(50) | NOT NULL | mid |
| `bind_type` | varchar(32) | NOT NULL | 绑定类型  GA |
| `bind_value` | varchar(60) | NOT NULL | 绑定值 |
| `status` | varchar(20) | NOT NULL | 状态  BOUND 已绑定; UNBOUND 已解绑; |
| `mobile_mask` | varchar(30) | NOT NULL | 手机号掩码 |
| `created_time` | timestamp | NOT NULL | 创建时间 |
| `last_updated_time` | timestamp | NOT NULL | 最后更新时间 |
| `data_version` | bigint | NOT NULL | 数据版本 |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `uk_mid_type` 唯一 (mid, bind_type)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

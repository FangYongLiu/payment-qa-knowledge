---
id: tbl_merchant_t_member_2fa_scene
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
- t_member_2fa_scene
subdomain: merchant
module: null
sensitivity: normal
name: 会员2fa场景(t_member_2fa_scene)
aliases:
- t_member_2fa_scene
related_services:
- svc_merchant
related_scenarios: []
---
# 会员2fa场景(t_member_2fa_scene)

## 用途
会员2fa场景。属 merchant 库,由 [[svc_merchant]] 读写。

## 关联关系
- **所属服务**:[[svc_merchant]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | id |
| `config_id` | bigint | NOT NULL | 2fa配置id |
| `scene` | varchar(32) | NOT NULL | 场景 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

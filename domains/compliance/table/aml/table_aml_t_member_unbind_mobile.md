---
id: tbl_aml_t_member_unbind_mobile
object_type: Table
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (aml schema) 2026-06-25
tags:
- aml
- aml
- t_member_unbind_mobile
subdomain: aml
module: null
sensitivity: normal
name: 会员解绑手机号(t_member_unbind_mobile)
aliases:
- t_member_unbind_mobile
related_services:
- svc_aml
related_scenarios: []
---
# 会员解绑手机号(t_member_unbind_mobile)

## 用途
会员解绑手机号。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | 主键 |
| `member_id` | varchar(32) | NOT NULL | 会员ID |
| `mobile` | varchar(20) | NOT NULL | 手机号 |
| `create_time` | timestamp |  | 创建时间 |

## 主键 / 索引
- 主键:(`id`)
- 唯一约束:
  - `memberIdMobile` 唯一 (member_id, mobile)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

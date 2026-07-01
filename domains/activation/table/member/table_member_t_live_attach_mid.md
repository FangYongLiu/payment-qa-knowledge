---
id: tbl_member_t_live_attach_mid
object_type: Table
domain: activation
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (member schema) 2026-06-25
tags:
- member
- config
- t_live_attach_mid
subdomain: config
module: null
sensitivity: normal
name: 活体附加会员表(t_live_attach_mid)
aliases:
- t_live_attach_mid
related_services:
- svc_member
related_scenarios: []
---

# 活体附加会员表(t_live_attach_mid)

## 用途
活体附加会员表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint(32) | PK |  |
| `member_id` | varchar(20) | NOT NULL | ID |
| `status` | char | NOT NULL |  |
| `memo` | varchar(150) |  |  |
| `create_time` | timestamp | NOT NULL |  |
| `update_time` | timestamp | NOT NULL |  |

## 主键 / 索引
- 主键:(`id`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

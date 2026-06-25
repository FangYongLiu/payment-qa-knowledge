---
id: tbl_member_tm_basic_card
object_type: Table
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (member schema) 2026-06-25
tags:
- member
- card-binding
- tm_basic_card
subdomain: card-binding
module: null
sensitivity: normal
name: 绑卡基础信息主表(tm_basic_card)
aliases:
- tm_basic_card
related_services:
- svc_member
related_scenarios: []
---

# 绑卡基础信息主表(tm_basic_card)

## 用途
绑卡基础信息主表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键 |
| `member_id` | varchar(20) | NOT NULL | 会员id |
| `identity` | varchar(64) |  | 外部用户标识 |
| `relation_id` | bigint | NOT NULL | 关联id |
| `card_category` | varchar(24) | NOT NULL | 卡类别 |
| `status` | tinyint(2) | NOT NULL | 1:有效；0无效 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

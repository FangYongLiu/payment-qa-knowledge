---
id: tbl_member_tm_member_address
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
- member-profile
- tm_member_address
subdomain: member-profile
module: null
sensitivity: normal
name: 会员地址表(tm_member_address)
aliases:
- tm_member_address
related_services:
- svc_member
related_scenarios: []
---

# 会员地址表(tm_member_address)

## 用途
会员地址表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint(30) | PK / NOT NULL | 主键 |
| `member_id` | varchar(32) | NOT NULL | 会员ID |
| `type` | varchar(20) |  | 地址类型,例：PASSPORT，EID，HOME |
| `room` | varchar(355) |  | 室 |
| `building` | varchar(355) |  | 建筑 |
| `street` | varchar(355) |  | 街道 |
| `area` | varchar(355) |  | 区域 |
| `city` | varchar(355) |  | 城市 |
| `province` | varchar(255) |  | 省份（洲） |
| `country` | varchar(355) |  | 国家 |
| `post_code` | varchar(15) |  | 邮政编号 |
| `is_default` | char |  | 是否默认（Y，N） |
| `enable` | char |  | 是否可用（Y，N） |
| `create_time` | timestamp |  | 创建时间 |
| `update_time` | timestamp |  | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

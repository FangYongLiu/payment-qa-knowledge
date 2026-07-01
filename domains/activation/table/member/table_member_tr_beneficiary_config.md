---
id: tbl_member_tr_beneficiary_config
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
- beneficiary
- tr_beneficiary_config
subdomain: beneficiary
module: null
sensitivity: normal
name: 受益人配置表(tr_beneficiary_config)
aliases:
- tr_beneficiary_config
related_services:
- svc_member
related_scenarios: []
---

# 受益人配置表(tr_beneficiary_config)

## 用途
受益人配置表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint(32) | PK | 主键 |
| `country_name` | varchar(200) | NOT NULL | 国家名称 |
| `country_code` | varchar(55) | NOT NULL | 国家code |
| `currency` | varchar(3) | NOT NULL | 币种 |
| `beneficiary_type` | varchar(20) | NOT NULL | 受益人类型 |
| `beneficiary_name` | varchar(35) | NOT NULL | 受益人名称（对外） |
| `clear_net` | varchar(16) |  | 清算网路 |
| `enable` | char | NOT NULL | 是否可用（Y，N） |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。

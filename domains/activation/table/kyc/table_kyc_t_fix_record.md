---
id: tbl_kyc_t_fix_record
object_type: Table
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-24'
source_type: DB DDL
source_ref: DataGrip DDL export (kyc schema) 2026-06-24
tags:
- kyc
- infra
- t_fix_record
subdomain: infra
module: null
sensitivity: normal
name: 修复数据临时表(t_fix_record)
aliases:
- t_fix_record
related_services:
- svc_kyc
related_scenarios: []
---

# 修复数据临时表(t_fix_record)

## 用途
**数据修复临时表**:运维/订正数据时的临时记录(member_id+biz_type 复合主键)。**临时性质**,非主流程。

## 关联关系
- **所属服务**:[[svc_kyc]](gp078_kyc,= frontmatter `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 分析反向可达,本侧不重复列)。
- **哪些场景校验它**:待补(暂无直接关联场景对象)。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `member_id` | varchar(32) | PK / NOT NULL | 会员ID |
| `biz_type` | varchar(32) | PK / NOT NULL | 业务类型 |
| `field` | varchar(55) |  | 某个字段值 |
| `memo` | varchar(200) |  | 操作类型 |
| `create_time` | timestamp |  | 创建时间 |
| `update_time` | timestamp |  | 更新时间 |

## 主键 / 索引
- 主键:(`member_id`, `biz_type`)
- 索引 `idx_member_id`:(`member_id`)

## 校验点(QA 关注)
- 仅运维订正使用,不应被业务流程依赖。
- 复合主键(member_id,biz_type) 唯一。

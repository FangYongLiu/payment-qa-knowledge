---
id: tbl_kyc_leaf_alloc
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
- leaf_alloc
subdomain: infra
module: null
sensitivity: normal
name: leaf_alloc(leaf_alloc)
aliases:
- leaf_alloc
related_services:
- svc_kyc
related_scenarios: []
---

# leaf_alloc(leaf_alloc)

## 用途
**Leaf 发号器表**:美团 Leaf segment 分段发号(`biz_tag`/`max_id`/`step`),为 KYC 各业务表生成全局有序 ID。基础设施表。

## 关联关系
- **所属服务**:[[svc_kyc]](gp078_kyc,= frontmatter `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 分析反向可达,本侧不重复列)。
- **哪些场景校验它**:待补(暂无直接关联场景对象)。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `biz_tag` | varchar(128) | PK / NOT NULL / 默认 '' | sequence名称 |
| `max_id` | bigint | NOT NULL / 默认 1 | 当前序列最大值，亦即下次取值的初始值 |
| `step` | int | NOT NULL | 初始情况下在内存中缓冲的序列号个数，一般配置表为10，订单表为200以上，看订单量 |
| `description` | varchar(256) |  | 描述 |
| `update_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 更新时间 |

## 主键 / 索引
- 主键:(`biz_tag`)
- 索引:无(除主键外原文未定义)

## 校验点(QA 关注)
- `step` 配置合理(配置表~10,流水表大);max_id 单调递增不回退。
- 并发取号不重复;biz_tag 与使用方对应。

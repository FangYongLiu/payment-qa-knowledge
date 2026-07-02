---
id: tbl_kyc_tm_message_config
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
- notify
- tm_message_config
subdomain: notify
module: null
sensitivity: normal
name: 通知配置表(tm_message_config)
aliases:
- tm_message_config
related_services:
- svc_kyc
related_scenarios: []
---

# 通知配置表(tm_message_config)

## 用途
**通知内容配置表**:通知模板(标题/内容/规则/详情链接/状态)。被 tm_message_event 以 config_id 引用。配置类。

## 关联关系
- **所属服务**:[[svc_kyc]](gp078_kyc,= frontmatter `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补(暂无直接关联场景对象)。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键ID |
| `title` | varchar(255) | NOT NULL | 标题 |
| `content` | varchar(800) |  | 通知内容 |
| `content_rule` | varchar(255) |  | 内容规则（如取acs国际化中的） |
| `details_url` | varchar(125) |  | 详情链接 |
| `status` | varchar(5) | NOT NULL | 状态（是否有效） |
| `extension` | varchar(255) |  | 拓展字段 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(除主键外原文未定义)

## 校验点(QA 关注)
- `status` 有效性;content_rule 取 acs 国际化时占位符正确。
- 失效配置不应被事件引用。

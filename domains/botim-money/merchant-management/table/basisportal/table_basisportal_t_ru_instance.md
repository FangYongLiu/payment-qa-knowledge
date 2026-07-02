---
id: tbl_basisportal_t_ru_instance
object_type: Table
name: workflow runtime instance (t_ru_instance)
aliases: [t_ru_instance, basisportal.t_ru_instance]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: basisportal schema DDL
tags: [merchant-management, basisportal]
sensitivity: normal
related_services: []
---

# workflow runtime instance (t_ru_instance)

## 用途
物理表 `basisportal.t_ru_instance`,主键 `id`。workflow runtime instance。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(21) | 待补 |
| `workflow_id` | bigint(21) | workflow ID |
| `version` | varchar(16) | workflow version |
| `system_code` | varchar(32) | code of registered system |
| `category` | varchar(64) | catagory |
| `request_title` | varchar(255) | Request title · 可空 |
| `object_id` | varchar(32) | identifier of business data · 可空 |
| `cur_node_key` | varchar(32) | current node key · 可空 |
| `cur_node_name` | varchar(32) | current node name · 可空 |
| `applicant` | varchar(45) | account of applicant · 可空 |
| `request_time` | timestamp | reqeust time · 可空 |
| `update_by` | varchar(45) | account of modifier · 可空 |
| `update_time` | timestamp | update time · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_t_ru_instance_applicant`:applicant
- `idx_t_ru_instance_request_time`:request_time
- `idx_t_ru_instance_system_code`:system_code, category

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

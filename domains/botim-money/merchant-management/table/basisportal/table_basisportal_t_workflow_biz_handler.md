---
id: tbl_basisportal_t_workflow_biz_handler
object_type: Table
name: Business data handler (t_workflow_biz_handler)
aliases: [t_workflow_biz_handler, basisportal.t_workflow_biz_handler]
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

# Business data handler (t_workflow_biz_handler)

## 用途
物理表 `basisportal.t_workflow_biz_handler`,主键 `id`。Business data handler。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(21) | 待补 |
| `category_id` | bigint(21) | ID of category · 可空 |
| `identifier` | varchar(64) | The identifier of operation · 可空 |
| `identifier_desc` | varchar(255) | Description of operation · 可空 |
| `register_time` | timestamp | Register Time · 可空 |
| `update_time` | timestamp | Update Time · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

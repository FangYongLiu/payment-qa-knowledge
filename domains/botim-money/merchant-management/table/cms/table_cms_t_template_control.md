---
id: tbl_cms_t_template_control
object_type: Table
name: 模版控制表 (t_template_control)
aliases: [t_template_control, cms.t_template_control]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cms schema DDL
tags: [merchant-management, cms]
sensitivity: normal
related_services: []
---

# 模版控制表 (t_template_control)

## 用途
物理表 `cms.t_template_control`,主键 `id`。模版控制表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(17) | 主键 |
| `template_id` | bigint(17) | 模版ID |
| `user_tag` | varchar(100) | 用户标签 · 可空 |
| `partner_id` | varchar(20) | 商户号 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 |
| `create_user` | bigint | 创建用户 · 可空 |
| `modify_user` | bigint | 修改用户 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

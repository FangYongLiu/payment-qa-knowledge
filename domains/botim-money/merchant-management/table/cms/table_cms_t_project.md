---
id: tbl_cms_t_project
object_type: Table
name: 方案表 (t_project)
aliases: [t_project, cms.t_project]
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

# 方案表 (t_project)

## 用途
物理表 `cms.t_project`,主键 `project_code`。方案表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `project_code` | bigint(18) | 方案code |
| `project_name` | varchar(120) | 方案名称 · 可空 |
| `platform_type` | varchar(18) | 终端类型:ios,android |
| `host_app` | varchar(20) | 宿主平台：payby，totok-pay，botim-pay,ALL |
| `package_type` | varchar(12) | 包类型：SDK，APP，ALL · 可空 |
| `min_version` | varchar(16) | 最小版本号 · 可空 |
| `max_version` | varchar(16) | 最大版本号 · 可空 |
| `status` | tinyint | 是否有效:0-失效，1-有效 · 可空 |
| `audit_status` | tinyint | 审核状态:0-待审批，1-审批通过，2-审批驳回 · 可空 |
| `creator` | varchar(120) | 创建人 · 可空 |
| `auditor` | varchar(120) | 审核人 · 可空 |
| `audit_time` | timestamp | 审核时间 · 可空 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`project_code`
- `t_project_idk`:project_code

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

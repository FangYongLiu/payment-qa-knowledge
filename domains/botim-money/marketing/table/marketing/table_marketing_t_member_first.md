---
id: tbl_marketing_t_member_first
object_type: Table
name: 会员首次记录 (t_member_first)
aliases: [t_member_first, marketing.t_member_first]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: marketing schema DDL
tags: [marketing, marketing]
sensitivity: normal
related_services: []
---

# 会员首次记录 (t_member_first)

## 用途
物理表 `marketing.t_member_first`,主键 `member_id, scenario_code`。会员首次记录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `member_id` | varchar(200) | 会员id |
| `scenario_code` | varchar(50) | 场景代码 |

## 主键 / 索引
- 主键:`member_id, scenario_code`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

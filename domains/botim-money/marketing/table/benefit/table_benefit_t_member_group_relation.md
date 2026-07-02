---
id: tbl_benefit_t_member_group_relation
object_type: Table
name: t_member_group_relation (t_member_group_relation)
aliases: [t_member_group_relation, benefit.t_member_group_relation]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: benefit schema DDL
tags: [marketing, benefit]
sensitivity: normal
related_services: []
---

# t_member_group_relation (t_member_group_relation)

## 用途
物理表 `benefit.t_member_group_relation`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 分组关系id · 可空 |
| `member_id` | varchar(32) | 会员id |
| `group_id` | bigint | 分组id |
| `extension` | varchar(255) | 扩展信息 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- `idx_member_id`:member_id, group_id (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

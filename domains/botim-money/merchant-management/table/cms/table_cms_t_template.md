---
id: tbl_cms_t_template
object_type: Table
name: 模版表 (t_template)
aliases: [t_template, cms.t_template]
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

# 模版表 (t_template)

## 用途
物理表 `cms.t_template`,主键 `id`。模版表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(17) | 主键 |
| `code` | varchar(100) | 模版CODE 用户输入 |
| `name` | varchar(50) | 模版名称 |
| `template_type` | varchar(100) | 模板类型(用户红包/用户转账/营销红包/商户红包) |
| `cover_group_id` | bigint(17) | 红包封面组ID |
| `def_cover_id` | bigint(17) | 当前模版默认封面 · 可空 |
| `fix_amount` | decimal(15, 4) | 固定金额 · 可空 |
| `min_amount` | decimal(15, 4) | 最小金额 · 可空 |
| `max_amount` | decimal(15, 4) | 最大金额 · 可空 |
| `self_receive` | tinyint | 是否能自己领取, 1:可领取 0:不可 · 可空 |
| `count` | int | 数量 · 可空 |
| `type` | varchar(20) | 红包类型 · 可空 |
| `expire_duration` | int | 红包有效时长 分钟为单位 默认一天 · 可空 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 |
| `status` | tinyint | 状态 1:开启 0:关闭 |
| `create_user` | bigint | 创建用户 · 可空 |
| `modify_user` | bigint | 修改用户 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_module_code`:code (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

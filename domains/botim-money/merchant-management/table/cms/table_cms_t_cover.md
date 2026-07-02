---
id: tbl_cms_t_cover
object_type: Table
name: 封面表 (t_cover)
aliases: [t_cover, cms.t_cover]
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

# 封面表 (t_cover)

## 用途
物理表 `cms.t_cover`,主键 `id`。封面表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(17) | 主键 |
| `name` | varchar(100) | 封面名称 |
| `type` | varchar(50) | 封面类型 |
| `regards` | varchar(200) | 祝福语 · 可空 |
| `begin_time` | timestamp | 生效时间 |
| `end_time` | timestamp | 失效时间 |
| `status` | tinyint | 状态 1:开启 0:关闭 |
| `currency` | varchar(10) | 币种 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 |
| `create_user` | bigint | 创建用户 · 可空 |
| `modify_user` | bigint | 修改用户 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

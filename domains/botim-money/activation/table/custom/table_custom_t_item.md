---
id: tbl_custom_t_item
object_type: Table
name: t_item (t_item)
aliases: [t_item, custom.t_item]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: custom schema DDL
tags: [activation, custom]
sensitivity: normal
related_services: []
---

# t_item (t_item)

## 用途
物理表 `custom.t_item`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | id · 可空 |
| `title` | varchar(100) | 标题 · 可空 |
| `item_type` | varchar(32) | item项类型 |
| `item_sub_type` | varchar(32) | item项子类 · 可空 |
| `item_attr` | varchar(16) | item属性（fix:固定 decorate:装饰） · 可空 |
| `item_condition` | varchar(150) | item匹配条件 · 可空 |
| `item_configure` | varchar(500) | item配置 · 可空 |
| `position` | int(1) | 扩展位置 0:首位  -1：末位 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

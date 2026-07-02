---
id: tbl_protocol_t_sys_dict
object_type: Table
name: 系统字典表 (t_sys_dict)
aliases: [t_sys_dict, protocol.t_sys_dict]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: protocol schema DDL
tags: [wallet, protocol]
sensitivity: normal
related_services: []
---

# 系统字典表 (t_sys_dict)

## 用途
物理表 `protocol.t_sys_dict`,主键 `id`。系统字典表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键ID · 可空 |
| `name` | varchar(255) | 名称 · 可空 |
| `type` | varchar(255) | 类型 · 可空 |
| `sub_type` | varchar(255) | 子类型 · 可空 |
| `dict_key` | varchar(255) | 键 · 可空 |
| `value` | varchar(800) | 值 · 可空 |
| `sort` | varchar(15) | 排序 · 可空 |
| `enable` | char | 是否可用， Y：可用， N：不可用 |
| `memo` | varchar(255) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

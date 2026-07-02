---
id: tbl_fiserv_t_reg_url
object_type: Table
name: 注册URL关系表 (t_reg_url)
aliases: [t_reg_url, fiserv.t_reg_url]
domain: offline-business
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: fiserv schema DDL
tags: [offline-business, fiserv]
sensitivity: normal
related_services: []
---

# 注册URL关系表 (t_reg_url)

## 用途
物理表 `fiserv.t_reg_url`,主键 `id`。注册URL关系表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 自增ID · 可空 |
| `reg_id` | bigint | t_registration表的id · 可空 |
| `url` | varchar(255) | URL · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

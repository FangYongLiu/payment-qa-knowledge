---
id: tbl_npss_t_maintain
object_type: Table
name: 维护表 (t_maintain)
aliases: [t_maintain, npss.t_maintain]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: npss schema DDL
tags: [payment-core, npss]
sensitivity: normal
related_services: []
---

# 维护表 (t_maintain)

## 用途
物理表 `npss.t_maintain`,主键 `maintain_id`。维护表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `maintain_id` | bigint(19) | Maintain id |
| `bic` | varchar(11) | bank identify code(swift code) |
| `status` | char | Maintain status, A-available, U-unavailable |
| `gmt_start` | timestamp | 开始时间 |
| `gmt_end` | timestamp | 结束时间 |
| `memo` | varchar(128) | Memo · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`maintain_id`
- `idx_maintain_bic`:bic

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

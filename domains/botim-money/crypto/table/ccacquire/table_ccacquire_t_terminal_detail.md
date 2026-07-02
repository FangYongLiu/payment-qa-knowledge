---
id: tbl_ccacquire_t_terminal_detail
object_type: Table
name: 终端信息 (t_terminal_detail)
aliases: [t_terminal_detail, ccacquire.t_terminal_detail]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ccacquire schema DDL
tags: [crypto, ccacquire]
sensitivity: normal
related_services: []
---

# 终端信息 (t_terminal_detail)

## 用途
物理表 `ccacquire.t_terminal_detail`,主键 `global_id`。终端信息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint | 全局号 |
| `operator_id` | varchar(200) | 待补 · 可空 |
| `terminal_id` | varchar(200) | 待补 · 可空 |
| `terminal_type` | varchar(50) | 待补 · 可空 |
| `store_id` | varchar(200) | 待补 · 可空 |
| `store_name` | varchar(200) | 待补 · 可空 |
| `merchant_name` | varchar(200) | 待补 · 可空 |
| `location` | varchar(200) | 待补 · 可空 |

## 主键 / 索引
- 主键:`global_id`
- `i_td_str`:store_id
- `i_td_t`:terminal_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

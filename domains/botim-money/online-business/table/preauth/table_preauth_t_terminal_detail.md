---
id: tbl_preauth_t_terminal_detail
object_type: Table
name: 终端信息 (t_terminal_detail)
aliases: [t_terminal_detail, preauth.t_terminal_detail]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: preauth schema DDL
tags: [online-business, preauth]
sensitivity: normal
related_services: [svc_preauth]
---

# 终端信息 (t_terminal_detail)

## 用途
物理表 `preauth.t_terminal_detail`,主键 `global_id`。终端信息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint | 全局号 |
| `operator_id` | varchar(200) | operator_id · 可空 |
| `terminal_id` | varchar(200) | terminal_id · 可空 |
| `store_id` | varchar(200) | store_id · 可空 |
| `store_name` | varchar(200) | store_name · 可空 |
| `merchant_name` | varchar(200) | merchant_name · 可空 |
| `location` | varchar(200) | location · 可空 |

## 主键 / 索引
- 主键:`global_id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

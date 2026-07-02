---
id: tbl_acquire_t_ugc_terminal
object_type: Table
name: 用户生成终端信息 (t_ugc_terminal)
aliases: [t_ugc_terminal, acquire.t_ugc_terminal]
domain: offline-business
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: acquire schema DDL
tags: [offline-business, acquire]
sensitivity: normal
related_services: []
---

# 用户生成终端信息 (t_ugc_terminal)

## 用途
物理表 `acquire.t_ugc_terminal`,主键 `global_id`。用户生成终端信息。业务语义细节**待补**(表结构来自 DDL)。

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
| `store_id` | varchar(200) | 待补 · 可空 |
| `store_name` | varchar(200) | 待补 · 可空 |
| `merchant_name` | varchar(200) | 待补 · 可空 |
| `location` | varchar(128) | 地址 · 可空 |

## 主键 / 索引
- 主键:`global_id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_acquire_terminal
object_type: Table
domain: pos-business
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_acquire_terminal.md
tags:
- 收单
- 终端
subdomain: null
module: null
sensitivity: normal
name: 收单终端表
aliases:
- t_acquire_terminal
- acquireii.t_acquire_terminal
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
记录收单订单关联的**终端基础信息**。表名 `acquireii.t_acquire_terminal`，业务含义为收单终端。与 `t_terminal_detail` 类似但字段更少，可能用于不同业务场景。

## 关键列
| 字段 | 类型 | 说明 |
|------|------|------|
| `global_id` | bigint | **主键**，对应订单 global_id |
| `terminal_id` | varchar(200) | 终端 ID |
| `terminal_type` | varchar(50) | 终端类型 |
| `store_id` | varchar(200) | 门店 ID |

## 主键/索引
- 主键：`global_id`
- 索引：
  - PRIMARY (global_id) — 主键

关联：与 `t_acquire_order` 为 1:1，关联字段 `global_id`。

## 校验点(QA 关注)
1. **与 t_terminal_detail 重复性**：注意业务上为什么有两张表，关注两者使用场景的差异。
2. **terminal_id 关联到 POS 设备**：核对 `terminal_id` 是否能正确映射到对应 POS 设备。
3. 通过 `global_id` 与 `t_acquire_order` 1:1 关联，校验订单与终端记录一致性。

常用查询：
```sql
SELECT * FROM t_acquire_terminal WHERE global_id = ?;
```

---
id: tbl_acquireii_t_terminal_detail
object_type: Table
domain: pos-business
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_terminal_detail.md
tags:
- pos
- 终端
- 门店
subdomain: null
module: null
sensitivity: normal
name: 终端明细表
aliases:
- t_terminal_detail
- acquireii.t_terminal_detail
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
记录订单来自哪个终端 / 门店 / 操作员。常见于 POS、门店收银场景。表名 `acquireii.t_terminal_detail`，与 `t_acquire_order` 通过 `global_id` 形成 1:1 关联。

## 关键列
| 字段 | 类型 | 说明 |
|------|------|------|
| `global_id` | bigint | 主键，对应订单 global_id |
| `operator_id` | varchar(200) | 操作员 ID（收银员） |
| `terminal_id` | varchar(200) | 终端 ID（POS 设备号） |
| `terminal_type` | varchar(50) | 终端类型 |
| `store_id` | varchar(200) | 门店 ID |
| `store_name` | varchar(200) | 门店名 |
| `merchant_name` | varchar(200) | 商户名 |
| `location` | varchar(200) | 位置 |

## 主键/索引
- PRIMARY：`global_id`
- `i_td_t`：`terminal_id`，按终端查
- `i_td_str`：`store_id`，按门店查

## 校验点(QA 关注)
1. **POS 场景才有数据**：线上订单 `t_terminal_detail` 可能没有记录，校验时不要默认存在。
2. **operator_id 用于审计**：用于门店收银员追溯。
3. **terminal_id 一致性**：`t_terminal_detail.terminal_id` 与 `t_acquire_terminal.terminal_id` 是同一个。
4. 与 `t_acquire_order` 关联应保持 1:1（按 `global_id`）。

---
id: tbl_acquireii_t_command_param
object_type: Table
domain: pos-business
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_command_param.md
tags:
- 分区表
- KV扩展
subdomain: null
module: null
sensitivity: normal
name: 指令参数表
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
`acquireii.t_command_param` 为 `t_command` 提供扩展参数存储（KV 结构）。指令执行所需的参数（如目标 URL、重试次数、超时配置等）以 pkey/value 形式存放。表注释标注"(分区)"，说明可能使用 MySQL 分区。

## 关键列
| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `id` | bigint | ✅ | 联合主键，对应 `t_command.id` |
| `pkey` | varchar(50) | ✅ | 联合主键，参数键 |
| `value` | varchar(200) | ✅ | 参数值 |

## 主键/索引
- PRIMARY KEY: `(id, pkey)` 联合主键
- 关联：`t_command` (N:1，关联字段 `id`)

## 校验点(QA 关注)
1. **表分区**：注释提示已分区，可能按 `id` 分区，查询条件应带上 `id` 以利分区裁剪。
2. **pkey 由指令类型定义**：不同 category 的指令参数集不同，校验时需结合 `t_command` 的指令类型确认 pkey 是否齐备（如 `notify_url`、`retry_count`、`timeout` 等）。
3. **value 长度限制 200**：超长值需要拆分存储，QA 需关注边界值。
4. **联合主键 (id, pkey)**：同一指令下 pkey 不可重复；插入相同 (id, pkey) 会冲突。
5. **与 t_command 一致性**：`id` 必须能在 `t_command` 找到对应记录，避免孤儿参数。

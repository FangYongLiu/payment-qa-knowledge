---
id: tbl_acquireii_t_command_param
object_type: Table
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
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
related_services:
- svc_acquireii
---

## 表用途
`acquireii.t_command_param` 是**指令参数表**，为 `t_command`（指令表）提供扩展参数的 KV 存储。指令在执行时所需的各类配置参数（如目标 URL、重试次数、超时配置、回调地址等）以 `pkey/value` 形式存放于本表。表注释标注"(分区)"，提示该表使用 MySQL 分区，查询时建议带上分区键以利于分区裁剪。

## 在交易链路中的位置
收单交易主单（`t_acquire_order` 等）在生命周期中会派发出多种指令（通知商户、发起退款、对账等），这些指令统一记录于 `t_command`，并按可重试/不可重试分别存于 `t_retryable_command`、`t_unretryable_command`。指令所需的参数集合不固定（不同 category 参数不同），因此采用本表以 KV 形式承载，避免主表字段膨胀。

链路示意：
- `t_acquire_order` / 其他业务订单 → 触发指令 → `t_command`（1）→ `t_command_param`（N，按 pkey 展开）→ 指令调度器读取参数执行
- 与 `t_event_param` 类似，均为 KV 扩展参数表，但服务对象分别为指令与事件。

## 关键列
| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `id` | bigint | ✅ | 联合主键，对应 `t_command.id` |
| `pkey` | varchar(50) | ✅ | 联合主键，参数键 |
| `value` | varchar(200) | ✅ | 参数值 |

## 主键/索引
- PRIMARY KEY：`(id, pkey)` 联合主键
- 分区：表注释提示已分区，疑似按 `id` 分区

## 关联关系
| 关联表 | 关系 | 关联字段 | 说明 |
|--------|------|----------|------|
| `t_command` | N:1 | `id` ↔ `t_command.id` | 主表，本表为其参数扩展 |
| `t_retryable_command` | 间接 | 通过 `t_command.id` | 可重试指令也共享本表参数 |
| `t_unretryable_command` | 间接 | 通过 `t_command.id` | 不可重试指令同上 |
| `t_event_param` | 同构 | — | 同为 KV 扩展参数表，结构参考一致 |

## QA 落库检查要点
1. **分区裁剪**：表已分区，QA 在校验/查询时 SQL 应携带 `id` 条件，避免全分区扫描。
2. **pkey 齐备性**：不同 category 的指令所需 pkey 集合不同，需结合 `t_command` 的指令类型逐一核对（如 `notify_url`、`retry_count`、`timeout`、回调签名等）是否齐备且无遗漏。
3. **value 长度边界 200**：`value` 长度上限 200 字符，超长值需要拆分或外部存储；QA 需覆盖边界与超长用例，确认不被截断。
4. **联合主键唯一性**：同一 `id` 下 `pkey` 不可重复；重复插入会主键冲突，需校验业务侧幂等处理。
5. **与 `t_command` 一致性**：每条 `id` 必须能在 `t_command` 中找到对应记录，禁止孤儿参数；指令删除/归档时参数表是否同步处理也应核查。
6. **必填非空**：`id`、`pkey`、`value` 三列均非空，落库时不允许 NULL。
7. **与同构表对照**：参数语义可参考 `t_event_param`，避免 KV 命名风格漂移。
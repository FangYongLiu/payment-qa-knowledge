---
id: tbl_acquireii_t_reversal_orderii
object_type: Table
domain: device-pos
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_reversal_orderii.md
tags:
- reversal
- orderii
- acquireii
subdomain: acquireii
module: reversal
sensitivity: normal
name: Reversal Order II 表
aliases:
- acquireii.t_reversal_orderii
- t_reversal_orderii
related_services: []
related_tables:
- tbl_acquireii_t_acquire_order
- tbl_acquireii_t_channel_param
- tbl_acquireii_t_command
- tbl_acquireii_t_refund_order
- tbl_acquireii_t_retryable_command
- tbl_acquireii_t_reversal_order
- tbl_acquireii_t_revoke_order
- tbl_acquireii_t_void_order
related_scenarios:
- scn_merchant_transaction_db_check
- scn_mit_autodebit
- scn_mit_cit_directpay_first
- scn_mit_cit_directpay_subsequent
- scn_mit_cit_payandsign
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

`acquireii.t_reversal_orderii` 是 reversal(冲正) 订单的升级版表，是 `t_reversal_order` 的新版本，业务含义为 reversal orderii。相比老表，新增 `channel_param_id` 字段用于关联具体的渠道参数 (`t_channel_param`)，实现 reversal 订单与渠道参数的精细化追踪关联。

**新表 vs 老表**：
- `t_reversal_order` —— 老版本，结构简单，存量旧渠道继续使用
- `t_reversal_orderii` —— 新版本，关联渠道参数，支持精细化追踪

**使用原则**：新业务和新接入的渠道必须使用 orderii 表。

## 在交易链路中的位置

Reversal(冲正) 是收单交易在通讯异常 / 超时等情况下，主动向渠道发送的逆向操作，用于消除前一笔不确定结果的支付指令。链路定位：

1. 上游来源：收单订单主表 `t_acquire_order` 在执行支付/预授权/撤销/退款过程中遇到通讯异常时，触发 reversal 流程。
2. 指令载体：reversal 通过 `t_command` / `t_retryable_command` 下发到渠道，与 `t_channel_param` 中的渠道配置一一绑定。
3. 本表落库：每一笔 reversal 操作的状态、错误码、关联渠道参数记录在 `t_reversal_orderii` 中。
4. 关联兄弟表：`t_revoke_order`(冲正订单)、`t_void_order`(撤销订单)、`t_refund_order`(退款订单) 共同构成支付逆向链路。

## 关键列

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `global_id` | bigint | ✅ | 主键，全局号 |
| `status` | varchar(32) |  | reversal 状态 |
| `fail_code` | varchar(50) |  | 错误码 |
| `fail_message` | varchar(200) |  | 错误描述 |
| `channel_param_id` | bigint |  | 渠道参数 ID(新增字段，关联 `t_channel_param.id`) |
| `created_time` | timestamp(3) | ✅ | 创建时间 |
| `last_updated_time` | timestamp(3) | ✅ | 最后更新时间 |
| `data_version` | bigint | ✅ | 数据版本(乐观锁) |

## 主键/索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | `global_id` | 主键 |
| `i_ro2_ct` | `created_time` | 按时间查询 |

## 关联关系

| 关联表 | 关系 | 关联字段 | 说明 |
|--------|------|----------|------|
| `t_channel_param` | N:1 | `channel_param_id` → `t_channel_param.id` | 获取 channel_code / channel_tid / trace_no 等渠道维度信息 |
| `t_acquire_order` | N:1(逻辑) | 通过 `global_id` 业务关联 | 上游被冲正的收单订单 |
| `t_command` / `t_retryable_command` | 1:N(逻辑) | 通过 `global_id` 业务关联 | reversal 指令下发记录 |
| `t_reversal_order` | 互斥 | — | 老表，仅存量旧渠道使用 |

## 校验点(QA 关注)

1. **优先使用 orderii 而不是 order**：新业务和新接入渠道必须落入 `t_reversal_orderii`，验证写入路径未走老表 `t_reversal_order`，避免双写或漏写。
2. **`channel_param_id` 可能为 NULL**：旧渠道存在兼容场景，关联查询需使用 `LEFT JOIN t_channel_param`，避免 INNER JOIN 导致旧渠道 reversal 记录丢失。
3. **关联字段一致性**：通过 `channel_param_id` JOIN `t_channel_param` 取 channel_code / channel_tid / trace_no 时，校验关联字段是否正确写入，与 `t_acquire_order` 上对应字段一致。
4. **status / fail_code / fail_message 三字段一致性**：失败状态下 fail_code、fail_message 应有值；成功状态下不应残留错误信息。
5. **乐观锁校验**：`data_version` 用于乐观锁，更新时需校验版本递增，并发更新不丢失。
6. **时间字段精度**：`created_time` / `last_updated_time` 为必填，timestamp(3) 精度到毫秒；`last_updated_time >= created_time`。
7. **链路完整性**：触发 reversal 的收单订单(`t_acquire_order`)应可通过 `global_id` 反查到本表记录，且 `t_command` 中应有对应指令落库。

---
id: tbl_acquireii_t_preauth_relation
object_type: Table
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_preauth_relation.md
tags:
- 预授权
- capture
- 关系表
subdomain: preauth
module: null
sensitivity: normal
name: 预授权关系表 t_preauth_relation
aliases:
- acquireii.t_preauth_relation
related_services:
- svc_acquireii
---

## 用途

`t_preauth_relation`（预授权关系表）记录**预授权（preauth）与实际扣款（capture）之间的关联明细**。一笔预授权可以多次 capture，每次 capture 在本表生成一条记录，是预授权场景的 capture 明细表。

例：预授权金额 1000，分 3 次 capture（400 + 300 + 300），本表对应 3 条记录，每条记录对应一次 capture。

## 在交易链路中的位置

预授权（Pre-Authorization）业务由两张表协同表达：

- `t_preauth_control`：**汇总/控制表**，按预授权订单维度记录授权总额、已 capture 总额、剩余可 capture 金额等汇总字段（每笔预授权 1 条）。
- `t_preauth_relation`（本表）：**明细表**，记录每一次 capture 操作对应的金额、币种、退款状态等（每次 capture 1 条，N:1 关联到 control）。

每次 capture 同时也是一笔独立的收单订单，因此本表 `global_id` 与 `t_acquire_order.global_id` 1:1 对应，可继续串联到 `t_payment_info`、`t_amount_detail`、`t_refund_order` 等下游表。

链路示意：

```
预授权请求 → t_preauth_control (1)
                 │
                 │ preauth_order_id
                 ▼
            t_preauth_relation (N) ── global_id ──▶ t_acquire_order ──▶ t_payment_info / t_amount_detail
                                                              │
                                                              └──▶ t_refund_order（capture 后退款）
```

## 关键列

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `global_id` | bigint | ✅ | 主键，本次 capture 的 global_id（同时也是一笔 acquire 订单的 global_id） |
| `amount` | decimal(19,4) | ✅ | 本次 capture 金额 |
| `amount_currency` | char(3) | ✅ | 币种 |
| `partner_id` | varchar(64) | ✅ | 商户 ID |
| `preauth_order_id` | bigint | ✅ | **关联到预授权订单的 global_id**（关键关联字段） |
| `refunded` | varchar(3) | ✅ | 是否已退款（Y/N） |
| `authorization_id` | varchar(64) |  | 授权 ID |
| `created_time` | timestamp(3) | ✅ | 创建时间 |
| `last_updated_time` | timestamp(3) | ✅ | 最后更新时间 |
| `data_version` | bigint | ✅ | 数据版本 |

## 主键 / 索引

- PRIMARY：`global_id`
- `i_pr_ct`：`created_time`，按时间查询
- `i_pr_poid`：`preauth_order_id`，**最常用索引**——通过预授权 ID 反查所有 capture 明细

## 关联关系

| 关联表 | 基数 | 关联字段 | 含义 |
|--------|------|----------|------|
| `t_preauth_control` | N:1 | `t_preauth_relation.preauth_order_id` → `t_preauth_control.global_id` | 多条 capture 明细汇总到一笔预授权 |
| `t_acquire_order` | 1:1 | `global_id` = `global_id` | 每次 capture 是一笔独立 acquire 订单 |
| `t_refund_order` | 1:N | 通过本表 `global_id` 作为被退款订单 | capture 后可退款，触发 `refunded=Y` |
| `t_payment_info` / `t_amount_detail` | 1:1 / 1:N | 通过 `global_id` | capture 订单的支付与金额明细 |

## QA 落库检查要点

1. **明细 vs 汇总一致性**：同一 `preauth_order_id` 下，本表所有记录的 `amount` 之和应等于 `t_preauth_control.captured_amount`（核对时需明确口径：是否仅统计 `refunded=N` 的记录）。
2. **多次 capture 场景**：业务允许一笔预授权对应多条本表记录，需验证部分 capture、多次部分 capture 场景下条数与金额数据完整。
3. **退款标识**：`refunded=Y` 表示该笔 capture 已退款；计算"有效已扣金额"时应排除 `refunded=Y` 的记录，并与 `t_refund_order` 的退款记录相互印证。
4. **关联字段非空且可达**：`preauth_order_id` 必须能在 `t_preauth_control` 中找到对应预授权记录，否则属于脏数据。
5. **币种一致性**：本表 `amount_currency` 应与对应预授权订单（`t_preauth_control`）及商户配置币种一致；同一 `preauth_order_id` 下多次 capture 的币种必须一致。
6. **`global_id` 双重身份**：`global_id` 既是本表主键，也应在 `t_acquire_order` 中存在对应订单记录（1:1），且 `partner_id`、`amount`、`amount_currency` 应与 `t_acquire_order` 一致。
7. **金额边界**：单次 capture `amount` 应 > 0 且 ≤ 预授权剩余可扣金额，所有 capture 金额累计不超过预授权授权总额。
8. **时间顺序**：`created_time` 应晚于对应 `t_preauth_control` 中预授权订单的创建时间。

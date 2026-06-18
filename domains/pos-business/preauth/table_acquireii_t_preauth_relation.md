---
id: tbl_acquireii_t_preauth_relation
object_type: Table
domain: pos-business
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
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
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
记录**预授权（preauth）与实际扣款（capture）之间的关联明细**。一笔预授权可以多次 capture，每次 capture 在本表生成一条记录。

例：预授权 1000，分 3 次 capture（400 + 300 + 300），本表对应 3 条记录，每条记录对应一次 capture。

本表为 capture 明细表，与汇总表 `t_preauth_control` 配合使用。

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

## 主键/索引
- PRIMARY：`global_id`
- `i_pr_ct`：`created_time`，按时间查询
- `i_pr_poid`：`preauth_order_id`，**常用索引**——通过预授权 ID 反查所有 capture 明细

关联关系：
- `t_preauth_control` N:1 — `preauth_order_id` → `global_id`
- `t_acquire_order` 1:1 — `global_id`（每次 capture 同时是一笔 acquire 订单）

## 校验点(QA 关注)
1. **明细 vs 汇总一致性**：同一 `preauth_order_id` 下，所有记录 `amount` 之和应等于 `t_preauth_control.captured_amount`（含 refunded=N 的口径需明确）。
2. **多次 capture 支持**：业务允许一笔预授权对应多条本表记录，验证多次部分 capture 场景下数据完整。
3. **退款标识**：`refunded = Y` 表示该笔 capture 已退款；计算"有效已扣金额"时应排除 `refunded = Y` 的记录。
4. **关联字段非空**：`preauth_order_id` 必须能在 `t_preauth_control` 中找到对应预授权记录，否则属于脏数据。
5. **币种一致性**：本表 `amount_currency` 应与对应预授权订单及商户币种一致。
6. **global_id 双重身份**：`global_id` 既是本表主键，也应在 `t_acquire_order` 中存在对应订单记录（1:1）。

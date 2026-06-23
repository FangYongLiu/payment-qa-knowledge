---
id: tbl_acquireii_t_revoke_order_param
object_type: Table
domain: device-pos
status: archived
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_revoke_order_param.md
tags:
- KV
- 扩展参数
- 冲正
subdomain: acquireii
module: revoke
sensitivity: normal
name: 冲正订单参数表
aliases:
- t_revoke_order_param
- acquireii.t_revoke_order_param
related_services: []
related_tables:
- tbl_acquireii_t_acquire_order
- tbl_acquireii_t_command_param
- tbl_acquireii_t_event_param
- tbl_acquireii_t_pay_scene_param
- tbl_acquireii_t_reversal_order
- tbl_acquireii_t_revoke_order
related_scenarios:
- scn_merchant_transaction_db_check
related_logs: []
related_requirements: []
related_failures: []
---

## 表定位

`acquireii.t_revoke_order_param`（冲正订单参数表）是 `t_revoke_order` 的**扩展属性表**，采用 KV（Key-Value）设计存储冲正业务的扩展字段。每行一个键值对，用于容纳随渠道、场景而异的扩展参数，避免主表频繁变更结构。

## 在交易链路中的位置

收单交易主链路：`t_acquire_order`（收单主单）→ 触发冲正 → `t_revoke_order`（冲正订单）→ `t_revoke_order_param`（冲正扩展参数）。

- 冲正（revoke）通常发生在前端支付动作未收到明确结果或需要主动撤销时，与 `t_reversal_order`（Reversal）、`t_void_order`（撤销）属于同一类反向交易族，但语义和触发条件不同。
- 本表与 `t_revoke_order` 为 **N:1** 关系，通过 `global_id` 关联。
- 设计模式与 `t_command_param`、`t_event_param`、`t_pay_scene_param` 一致，都是主表 + KV 扩展参数表。

## 字段定义

| 字段 | 类型 | 是否必填 | 说明 |
|------|------|---------|------|
| `global_id` | bigint | ✅ | 联合主键，对应 `t_revoke_order.global_id` |
| `pkey` | varchar(200) | ✅ | 联合主键，参数键名 |
| `value` | varchar(200) | ✅ | 参数值 |

常见 pkey 示例（业务约定，无 schema 强约束）：`origin_order_id`、`channel_code`、`retry_count`。

## 主键/索引

- PRIMARY KEY：联合主键 `(global_id, pkey)`
- 外部关联：`global_id` → `t_revoke_order.global_id`（N:1）

## 与关联表的关系

| 关联表 | 关系 | 说明 |
|--------|------|------|
| `t_revoke_order` | N:1 | 主单，本表是其扩展参数。时间字段（创建/更新时间）需从主单关联获取 |
| `t_acquire_order` | 间接 | 通过 `t_revoke_order` 上的订单号回溯到原始收单订单 |
| `t_command_param` / `t_event_param` / `t_pay_scene_param` | 同模式 | 同为 KV 扩展参数表，结构与查询模式高度相似 |

## QA 落库检查要点

1. **关联完整性**：每条 `t_revoke_order` 记录如有扩展参数写入，需检查 `(global_id, pkey)` 是否齐全；常见 pkey（如 `origin_order_id`、`channel_code`）应能查到。
2. **value 长度受限 200**：长值需分段或改用其他存储，避免超长截断。校验时应关注 value 边界。
3. **没有时间字段**：本表无 `create_time` / `update_time`，插入时间需通过 `global_id` 回查 `t_revoke_order` 获取。
4. **pkey 无 schema 约束**：使用前需与业务方对齐键名清单，避免拼写大小写不一致（如 `originOrderId` vs `origin_order_id`）造成查询遗漏。
5. **联合主键唯一性**：同一 `global_id` 下相同 `pkey` 不能重复写入；若业务需要多值，应在 value 里序列化或新增 pkey 后缀。
6. **透视查询写法**：取多键时使用按 `global_id` 分组聚合：
   ```sql
   SELECT global_id,
          MAX(CASE WHEN pkey='origin_order_id' THEN value END) AS origin_order_id,
          MAX(CASE WHEN pkey='channel_code'    THEN value END) AS channel_code
   FROM acquireii.t_revoke_order_param
   WHERE global_id IN (...)
   GROUP BY global_id;
   ```
7. **联调反查**：对冲正异常排查时，应同时拉取 `t_revoke_order` + 本表 + `t_acquire_order`，定位冲正触发原因与渠道返回。

---
id: tbl_acquireii_t_revoke_order_param
object_type: Table
domain: pos-business
status: active
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
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
为 `t_revoke_order` 提供**扩展字段存储**，采用 KV 设计，每一行一个键值对。冲正业务参数随渠道、场景而异，固定字段不灵活，KV 形式可以容纳任意扩展参数而不需要改表结构。

表名：`acquireii.t_revoke_order_param`，业务含义为 revoke 订单参数。

## 关键列
| 字段 | 类型 | 是否必填 | 说明 |
|------|------|---------|------|
| `global_id` | bigint | ✅ | 联合主键，对应 `t_revoke_order.global_id` |
| `pkey` | varchar(200) | ✅ | 联合主键，参数键名 |
| `value` | varchar(200) | ✅ | 参数值 |

常见 pkey 示例（业务约定）：`origin_order_id`、`channel_code`、`retry_count`。

## 主键/索引
- PRIMARY：联合主键 `(global_id, pkey)`
- 关联：与 `t_revoke_order` 为 N:1，`global_id → global_id`

## 校验点(QA 关注)
1. **value 长度受限 200**：长值需要分段或使用其他存储，避免超长截断。
2. **没有时间字段**：插入时间需要从 `t_revoke_order` 关联查询获取。
3. **pkey 没有 schema 约束**：使用前要和业务方确认有哪些键，避免拼写不一致导致查询遗漏。
4. **联合主键唯一性**：同一 `global_id` 下相同 `pkey` 不能重复写入。
5. **透视查询场景**：取多键时建议使用 `MAX(CASE WHEN pkey = ... THEN value END)` 聚合方式按 `global_id` 分组。

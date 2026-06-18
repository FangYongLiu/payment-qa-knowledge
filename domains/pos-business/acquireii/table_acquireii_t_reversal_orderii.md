---
id: tbl_acquireii_t_reversal_orderii
object_type: Table
domain: pos-business
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
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

`acquireii.t_reversal_orderii` 是 reversal 订单的升级版表(`t_reversal_order` 的新版本)，业务含义为 reversal orderii。相比老表，新增 `channel_param_id` 字段用于关联具体的渠道参数(`t_channel_param`)，实现 reversal 订单与渠道参数的精细化追踪关联。

新表 vs 老表：
- `t_reversal_order` —— 老版本，结构简单
- `t_reversal_orderii` —— 新版本，关联渠道参数

新业务和新接入的渠道应使用 orderii 表。

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
| `data_version` | bigint | ✅ | 数据版本 |

## 主键/索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | `global_id` | 主键 |
| `i_ro2_ct` | `created_time` | 按时间查询 |

关联关系：与 `t_channel_param` 为 N:1，关联字段 `channel_param_id`。

## 校验点(QA 关注)

1. **优先使用 orderii 而不是 order**：新业务和新接入渠道必须落入 `t_reversal_orderii`，验证写入路径未走老表 `t_reversal_order`。
2. **`channel_param_id` 可能为 NULL**：旧渠道存在兼容场景，关联查询需使用 `LEFT JOIN t_channel_param`，避免 INNER JOIN 导致旧渠道 reversal 记录丢失。
3. 关联查询 channel_code / channel_tid / trace_no 时，需通过 `channel_param_id` JOIN `t_channel_param`，校验关联字段是否正确写入。
4. `status` / `fail_code` / `fail_message` 三字段一致性：失败状态下 fail_code、fail_message 应有值；成功状态下不应残留错误信息。
5. `data_version` 用于乐观锁校验，更新时需校验版本递增。
6. `created_time` / `last_updated_time` 为必填，timestamp(3) 精度到毫秒。

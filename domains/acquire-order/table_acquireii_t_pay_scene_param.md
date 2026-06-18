---
id: tbl_acquireii_t_pay_scene_param
object_type: Table
domain: acquire-order
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_pay_scene_param.md
tags:
- KV表
- 支付场景
- 扩展参数
subdomain: null
module: null
sensitivity: normal
name: 支付场景参数表
aliases:
- t_pay_scene_param
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

`acquireii.t_pay_scene_param` 表，存储一笔订单的**支付场景相关参数**，采用 KV（pkey/value）结构。

不同的 `pay_scene_code` 需要不同的扩展参数，固定字段无法穷举所有场景，故采用 KV 表设计：

- **PAYPAGE** 场景：需要 token、redirect_url、result_url
- **DEEPLINK** 场景：需要 app_scheme
- **ONETIME** 场景：需要 card_token

与 `t_acquire_order` 是 N:1 关系，关联字段为 `global_id`。

## 关键列

| 字段 | 类型 | 是否必填 | 说明 |
|------|------|---------|------|
| `global_id` | bigint | ✅ | 联合主键，对应订单 global_id |
| `pkey` | varchar(200) | ✅ | 联合主键，参数键 |
| `value` | varchar(255) |  | 参数值 |

**常见 pkey 示例**：
- `token_url`：PAYPAGE 跳转 URL
- `redirect_url`：支付完成跳转
- `notify_url`：异步通知
- `card_token`：卡令牌
- `app_scheme`：APP scheme

## 主键/索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | (global_id, pkey) | 联合主键 |

## 校验点(QA 关注)

1. **pkey 没有 schema 约束**：可能的 key 集合需查代码或业务文档了解，校验时需注意 pkey 命名是否与场景一致。
2. **value 长度限制 255**：长值（如较长的 URL、token）可能需拆分或换存储，需关注超长截断风险。
3. **场景与参数的匹配性**：不同 `pay_scene_code` 应写入对应的 pkey 集合（如 PAYPAGE 应有 token_url/redirect_url/result_url；ONETIME 应有 card_token；DEEPLINK 应有 app_scheme），缺失关键 key 会影响支付流程。
4. **联合主键唯一性**：同一 `global_id + pkey` 不可重复写入。

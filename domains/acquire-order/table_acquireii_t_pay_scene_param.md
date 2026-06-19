---
id: tbl_acquireii_t_pay_scene_param
object_type: Table
domain: acquire-transaction
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
related_tables:
- tbl_acquireii_t_acquire_order
- tbl_acquireii_t_card_info
- tbl_acquireii_t_channel_param
- tbl_acquireii_t_command_param
- tbl_acquireii_t_event_param
- tbl_acquireii_t_payment_info
related_scenarios:
- scn_acquire_product_apply
- scn_cko_standalone_card_binding
- scn_merchant_transaction_db_check
- scn_mit_cit_directpay_first
- scn_mit_cit_payandsign
related_logs: []
related_requirements: []
related_failures: []
---

## 表用途

`acquireii.t_pay_scene_param`（支付场景参数表）以 KV（pkey/value）结构存储一笔订单的**支付场景相关扩展参数**。由于不同的 `pay_scene_code`（支付场景码）所需扩展参数差异较大，固定列无法穷举，故使用 KV 表灵活承载。

典型场景与所需 pkey：
- **PAYPAGE**（收银台跳转）：`token_url`、`redirect_url`、`result_url`
- **DEEPLINK**（APP 唤起）：`app_scheme`
- **ONETIME**（一次性卡令牌支付）：`card_token`
- 通用可选：`notify_url`（异步通知）

## 在交易链路中的位置

下单（创建 `t_acquire_order`）阶段，根据请求中的 `pay_scene_code` 把对应场景需要的扩展参数拆解后写入本表；后续支付路由、跳转 URL 拼装、回跳/通知处理等环节会按 `global_id + pkey` 读取。

```
下单请求 → t_acquire_order(主单) ──┬─ t_pay_scene_param (本表, 场景KV参数)
                                  ├─ t_payment_info  (支付信息)
                                  ├─ t_card_info     (卡信息, ONETIME 等场景)
                                  └─ t_channel_param (渠道侧参数)
```

## 关联关系

| 关联表 | 关系 | 关联键 | 说明 |
|---|---|---|---|
| `t_acquire_order` | N:1 | `global_id` | 一笔订单可对应多行 KV 参数；`pay_scene_code` 在主表上 |
| `t_payment_info` | 同单关联 | `global_id` | 支付方式/状态信息，与场景参数共同决定支付走向 |
| `t_card_info` | 同单关联 | `global_id` | ONETIME 场景的 `card_token` 通常对应卡信息记录 |
| `t_channel_param` | 同单关联 | `global_id` | 渠道维度的扩展参数；与本表分别承载“场景维度 vs 渠道维度” |
| `t_command_param` / `t_event_param` | 同体系 KV 表 | - | 指令/事件维度的 KV 参数，设计风格相同 |

## 关键列

| 字段 | 类型 | 是否必填 | 说明 |
|------|------|---------|------|
| `global_id` | bigint | ✅ | 联合主键，对应 `t_acquire_order.global_id` |
| `pkey` | varchar(200) | ✅ | 联合主键，参数键 |
| `value` | varchar(255) |  | 参数值 |

**常见 pkey**：`token_url`、`redirect_url`、`result_url`、`notify_url`、`card_token`、`app_scheme`。

## 主键/索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | (`global_id`, `pkey`) | 联合主键，保证同单同 key 唯一 |

## QA 落库检查要点

1. **场景与 pkey 匹配性**：根据主表 `pay_scene_code` 校验本表是否写入了该场景应有的 pkey 集合：
   - PAYPAGE → `token_url` / `redirect_url` / `result_url` 齐全
   - DEEPLINK → `app_scheme` 必须存在
   - ONETIME → `card_token` 必须存在，且与 `t_card_info` 一致
   - 缺失关键 key 会直接导致支付页/跳转/扣款流程失败。
2. **pkey 无 schema 约束**：表层不限制 key 名称，命名拼写错误（如 `redirectUrl` vs `redirect_url`）排查时需对照代码或业务文档逐一核对。
3. **value 长度上限 255**：URL、token 等较长值需关注是否被截断；超长场景应评估改用其他存储或分段。
4. **联合主键唯一性**：同一 `global_id + pkey` 不可重复写入；幂等下单/重试时需校验是否走 upsert 而非重复 insert。
5. **与关联表一致性**：例如 ONETIME 的 `card_token` 应能在 `t_card_info` 中找到对应卡；`notify_url` 与 `t_acquire_order` 主表上的通知配置一致。
6. **空值/脏数据**：`value` 允许为空，但业务关键 pkey 不应为空字符串。
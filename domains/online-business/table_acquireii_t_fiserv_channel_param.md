---
id: tbl_acquireii_t_fiserv_channel_param
object_type: Table
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_fiserv_channel_param.md
tags:
- fiserv
- kv
- 渠道参数
subdomain: null
module: null
sensitivity: normal
name: Fiserv渠道参数表
aliases:
- acquireii.t_fiserv_channel_param
related_services:
- svc_acquireii
---

## 用途

`acquireii.t_fiserv_channel_param` 是 **Fiserv 渠道专属的扩展参数表**，采用 KV（键值）结构为接入 Fiserv 渠道的收单订单保存渠道相关的扩展信息（如渠道响应、授权码等）。它是通用渠道参数表 `t_channel_param` 在 Fiserv 渠道上的补充：当 Fiserv 集成需要存储一些不属于通用模型、但又需要按订单维度归档的字段时，统一落到本表。

## 在交易链路中的位置

```
收单下单 → t_acquire_order(主表, global_id)
        ├─ t_payment_info        支付/卡信息
        ├─ t_channel_param       通用渠道参数 (KV)
        └─ t_fiserv_channel_param  ← Fiserv 渠道扩展 (KV, 本表)
指令交互 → t_command / t_command_param
事件回执 → t_event_param
```

- 入口键统一是订单的 `global_id`（与 `t_acquire_order.global_id` 一致）。
- 仅在订单走 Fiserv 渠道（如测试环境构造 Fiserv TID 场景）时才会有数据写入。
- 与 `t_channel_param` 是**互补关系**而非替代：通用字段走 `t_channel_param`，Fiserv 私有字段走本表，避免污染通用表。

## 表结构

表名：`acquireii.t_fiserv_channel_param`

| 字段 | 类型 | 是否必填 | 说明 |
|------|------|---------|------|
| `global_id` | bigint | ✅ | 联合主键，订单 global_id，关联 `t_acquire_order.global_id` |
| `pkey` | varchar(50) | ✅ | 联合主键，参数键（由 Fiserv 集成定义，常见如 `channel_response`、`auth_code` 等） |
| `value` | varchar(200) | ✅ | 参数值 |

## 主键 / 索引

- PRIMARY KEY：`(global_id, pkey)` 联合主键，保证同一订单下每个参数键唯一。

## 常用查询

```sql
-- 取某订单的全部 Fiserv 渠道参数
SELECT pkey, value
FROM t_fiserv_channel_param
WHERE global_id = ?;

-- 取特定参数（如授权码）
SELECT value
FROM t_fiserv_channel_param
WHERE global_id = ? AND pkey = 'auth_code';
```

## QA 落库检查要点

1. **关联完整性**：`global_id` 必须能在 `t_acquire_order` 中查到对应订单，且订单渠道为 Fiserv，否则属脏数据。
2. **pkey 命名一致性**：`pkey` 由 Fiserv 集成定义，常见键包括 `channel_response`、`auth_code` 等。回归时需校验业务约定的 key 是否齐全、拼写是否一致（区分大小写、下划线风格）。
3. **value 长度上限 200**：长字段（如完整渠道报文）超过 200 需要拆分或改走其他存储；测试时关注截断风险。
4. **与通用 `t_channel_param` 的边界**：同一信息不应在两张表里重复落库；QA 需确认 Fiserv 私有字段只落本表，通用字段只落 `t_channel_param`。
5. **查询入口**：始终以 `global_id` 为入口按 KV 取出全部参数，不要用 `pkey` 单独全表扫。
6. **构造 TID 场景**：在 Fiserv TID 构造类测试场景中，需校验本表关键 key（如 `auth_code`）是否在收到 Fiserv 响应后正确写入。
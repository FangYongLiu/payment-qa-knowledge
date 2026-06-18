---
id: tbl_acquireii_t_fiserv_channel_param
object_type: Table
domain: pos-business
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
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
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
为 Fiserv 渠道的订单提供**扩展参数存储**，采用 KV 结构保存渠道相关扩展信息。

表名：`acquireii.t_fiserv_channel_param`

## 关键列
| 字段 | 类型 | 是否必填 | 说明 |
|------|------|---------|------|
| `global_id` | bigint | ✅ | 联合主键，订单 global_id |
| `pkey` | varchar(50) | ✅ | 联合主键，参数键（由 Fiserv 集成定义，常见如 channel_response、auth_code 等） |
| `value` | varchar(200) | ✅ | 参数值 |

## 主键/索引
- PRIMARY：`(global_id, pkey)` 联合主键

常用查询：
```sql
SELECT pkey, value
FROM t_fiserv_channel_param
WHERE global_id = ?;
```

## 校验点(QA 关注)
1. **pkey 由 Fiserv 集成定义**：常见键包括 channel_response、auth_code 等，需校验 key 命名一致性。
2. **value 长度上限 200**：超长值需要拆分存储，注意截断风险。
3. 查询应使用 `global_id` 作为入口，按 KV 取出全部参数。

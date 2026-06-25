---
id: tbl_acquireii_t_pcc_content_param
object_type: Table
name: 授权代码参数表 (acquireii.t_pcc_content_param)
aliases:
- t_pcc_content_param
- acquireii.t_pcc_content_param
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-25'
source_type: upload
source_ref: tables/t_pcc_content_param.md
tags:
- table
- authorization
- kv-params
related_services:
- svc_acquireii
related_scenarios: []
---

# 授权代码参数表 (acquireii.t_pcc_content_param)

## 用途

`acquireii.t_pcc_content_param`，业务含义为**授权代码参数**。为 `t_pcc_content`（授权凭证主表）提供**扩展字段存储**，以 KV（键值对）结构承载授权凭证的扩展参数。重要程度：⭐⭐。

## 关联关系

- **所属服务**：[[svc_acquireii]]（= frontmatter `related_services`，tbl→service 边）
- **关联表**：`t_pcc_content`（主表，N:1，通过 `global_id` 关联；该主表尚无 typed 对象，待补）

## 关键列

| 列 | 类型 | 必填 | 说明 |
|------|------|---------|------|
| `global_id` | bigint | ✅ | **联合主键**，对应 `t_pcc_content.global_id` |
| `pkey` | varchar(200) | ✅ | **联合主键**，参数键 |
| `value` | varchar(200) | ✅ | 参数值 |

## 主键 / 索引

- 主键：`PRIMARY (global_id, pkey)`（联合主键）。
- 关联：`t_pcc_content`（N:1，关联字段 `global_id`）。

常用查询（按 `global_id` 取某授权码的所有参数）：
```sql
SELECT pkey, value FROM t_pcc_content_param
WHERE global_id = ? ORDER BY pkey;
```

## 校验点(QA 关注)

1. **pkey 无 schema 约束**：使用前需确认存在哪些键，避免误用未知键。
2. **value 长度 200**：长值需分段存储。
3. 联合主键 `(global_id, pkey)` 决定同一 `global_id` 下 `pkey` 不可重复。
4. 与 `t_pcc_content` 通过 `global_id` 呈 N:1，需确保父表记录存在。

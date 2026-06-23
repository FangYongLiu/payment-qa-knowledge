---
id: tbl_pcc_content_param
object_type: Table
domain: authorization-protocol
status: archived
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_pcc_content_param.md
tags:
- table
- authorization
- kv-params
subdomain: null
module: null
sensitivity: normal
name: 授权代码参数表
aliases:
- t_pcc_content_param
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
- 表名：`acquireii.t_pcc_content_param`，业务含义为授权代码参数。
- 为 `t_pcc_content` 提供**扩展字段存储**，以 KV(键值对) 结构承载授权凭证的扩展参数。
- 重要程度：⭐⭐。

## 关键列
| 字段 | 类型 | 是否必填 | 说明 |
|------|------|---------|------|
| `global_id` | bigint | ✅ | **联合主键**，对应 `t_pcc_content.global_id` |
| `pkey` | varchar(200) | ✅ | **联合主键**，参数键 |
| `value` | varchar(200) | ✅ | 参数值 |

## 主键/索引
| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | (global_id, pkey) | 联合主键 |

关联表：
| 关联表 | 关系 | 关联字段 |
|--------|------|---------|
| `t_pcc_content` | N:1 | global_id |

常用查询：按 `global_id` 查询某授权码的所有参数：
```sql
SELECT pkey, value
FROM t_pcc_content_param
WHERE global_id = ?
ORDER BY pkey;
```

## 校验点(QA 关注)
1. **pkey 无 schema 约束**：使用前需确认存在哪些键，避免误用未知键。
2. **value 长度 200**：长值需要分段存储。
3. 联合主键 `(global_id, pkey)` 决定同一 `global_id` 下 `pkey` 不可重复。
4. 与 `t_pcc_content` 通过 `global_id` 关联，呈 N:1 关系，需确保父表记录存在。

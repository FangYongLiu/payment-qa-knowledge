---
id: tbl_acquire_extension
object_type: Table
domain: pos-business
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_acquire_extension.md
tags:
- extension
- 收单
subdomain: null
module: null
sensitivity: normal
name: 收单扩展表
aliases:
- t_acquire_extension
- acquireii.t_acquire_extension
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
为收单业务提供通用扩展信息存储，一般以 JSON 或自定义格式（序列化字符串）存储复杂业务数据。

- 表名：`acquireii.t_acquire_extension`
- 表注释：extension
- 业务含义：收单扩展信息
- 重要程度：⭐⭐

## 关键列

| 字段 | 类型 | 是否必填 | 说明 |
|------|------|---------|------|
| `id` | bigint | ✅ | 主键，global id |
| `extension` | varchar(255) | ✅ | 扩展数据（可能是 JSON / 序列化字符串） |
| `data_version` | bigint | ✅ | 数据版本 |
| `created_time` | timestamp(3) | ✅ | 创建时间 |
| `last_updated_time` | timestamp(3) | ✅ | 最后更新时间 |

## 主键/索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | id | 主键 |

常用查询：

```sql
SELECT * FROM t_acquire_extension WHERE id = ?;
```

## 校验点(QA 关注)

1. **extension 长度只有 255**：不能存大对象，写入前需校验长度，避免截断。
2. **没有明确 schema**：使用前需确认字段含义，extension 内容格式（JSON / 序列化字符串）依赖业务约定。
3. **data_version**：用于数据版本控制，更新时关注版本一致性。
4. **id 为 global id**：跨业务场景需确保 id 生成规则一致，避免冲突。

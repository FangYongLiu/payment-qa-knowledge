---
id: tbl_pos_settlement_history
object_type: Table
domain: pos-business
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_pos_settlement_history.md
tags:
- pos
- settlement
- history
- archive
subdomain: settlement
module: null
sensitivity: normal
name: POS结算历史表
aliases:
- t_pos_settlement_history
- acquireii.t_pos_settlement_history
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
存储 POS 设备**已完成的结算记录**的历史归档表。每完成一次结算就追加一条，用于查询设备结算历史和统计商户设备结算频率。

- 表名：`acquireii.t_pos_settlement_history`
- 业务含义：POS 结算历史记录
- 重要程度：⭐⭐⭐
- 关联表：`t_pos_settlement`（N:1，通过 `device_id` 关联）

## 关键列

| 字段 | 类型 | 必填 | 说明 |
|------|------|-----|------|
| `id` | bigint | ✅ | 主键 |
| `device_id` | varchar(32) | ✅ | 设备 ID |
| `partner_id` | varchar(32) | ✅ | 商户 ID |
| `start_time` | timestamp(3) | ✅ | 结算开始时间 |
| `end_time` | timestamp(3) | ✅ | 结算结束时间 |
| `operator_id` | varchar(50) | ✅ | 操作员 ID（审计字段）|
| `created_time` | timestamp(3) | ✅ | 创建时间 |

## 主键/索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | `id` | 主键 |

> 注：当前仅有主键索引，按 `device_id` / `partner_id` / `start_time` 的查询场景下需关注扫描成本。

## 校验点(QA 关注)

1. **追加表，不更新**：每条记录只读，每次结算完成后追加一条，禁止 UPDATE 历史记录。
2. **数据量持续增长**：建议按时间分区，避免历史表膨胀拖慢查询。
3. **operator_id 是审计字段**：必填，需校验来源的真实操作员，不能为空或伪造。
4. **常用查询场景**：
   - 设备结算历史：按 `device_id` 过滤 + `start_time DESC` 排序 + `LIMIT 30`，关注无 `device_id` 索引时的性能。
   - 商户设备结算频率统计：按 `partner_id` 过滤 + `device_id` 分组，统计 `COUNT(*)`、`MIN(start_time)`、`MAX(end_time)`。
5. **时间字段一致性**：`end_time` 应 ≥ `start_time`；`created_time` 应 ≥ `end_time`（结算完成后入库）。
6. **与 `t_pos_settlement` 的对应关系**：归档来源关系需保证 `device_id` 在主表中存在或曾经存在。

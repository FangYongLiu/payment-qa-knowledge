---
id: tbl_pos_settlement_history
object_type: Table
domain: device-pos
status: archived
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
related_tables:
- tbl_fiserv_batch
- tbl_fiserv_sale_order
- tbl_hardware_info
- tbl_merchant_device
- tbl_pos_settlement
related_scenarios:
- scn_merchant_transaction_db_check
- scn_pos_transaction_db_check
related_logs: []
related_requirements: []
related_failures: []
---

## 用途

`acquireii.t_pos_settlement_history` 存储 POS 设备**已完成的结算记录**，是 POS 结算流水的归档表。每当一次设备结算（批结/对账）完成，即向本表追加一条只读记录，用于：

- 按设备查询结算历史（设备维度审计）；
- 按商户统计设备结算频率（商户维度运营分析）；
- 与 `t_pos_settlement`（活跃结算主表）配合，承担长期归档职责。

- 表名：`acquireii.t_pos_settlement_history`
- 业务含义：POS 结算历史记录
- 重要程度：⭐⭐⭐

## 在交易链路中的位置

POS 交易链路（简化）：

1. 设备激活（`tbl_active_code` / `tbl_hardware_info` / `tbl_merchant_device`）
2. 设备发起销售/撤销/退款交易 → 落库到 `tbl_fiserv_sale_order` / `tbl_fiserv_sale_void_ops_order` / `tbl_fiserv_refund_order` / `tbl_fiserv_reversal_order`
3. 交易归集成批次 → `tbl_fiserv_batch`
4. 设备触发结算（批结） → 写入 `tbl_pos_settlement`
5. **结算完成后追加到 `tbl_pos_settlement_history`**（本表），主表中对应记录可清理或保留指针

本表处于链路末端，是结算闭环的最终落点。

## 关键列

| 字段 | 类型 | 必填 | 说明 |
|------|------|-----|------|
| `id` | bigint | ✅ | 主键 |
| `device_id` | varchar(32) | ✅ | 设备 ID，关联 `tbl_hardware_info` / `tbl_merchant_device` |
| `partner_id` | varchar(32) | ✅ | 商户 ID |
| `start_time` | timestamp(3) | ✅ | 结算开始时间 |
| `end_time` | timestamp(3) | ✅ | 结算结束时间 |
| `operator_id` | varchar(50) | ✅ | 操作员 ID（审计字段） |
| `created_time` | timestamp(3) | ✅ | 创建时间（追加入库时刻） |

## 主键/索引

| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | `id` | 主键 |

> 注：当前仅有主键索引，按 `device_id` / `partner_id` / `start_time` 的查询场景下需关注扫描成本，必要时建议补建二级索引或时间分区。

## 与关联表的关系

| 关联表 | 关系 | 关联键 | 说明 |
|--------|------|--------|------|
| `tbl_pos_settlement` | N:1（来源主表） | `device_id` | 本表的归档来源；同一设备在主表对应多次历史结算 |
| `tbl_merchant_device` | N:1 | `device_id` + `partner_id` | 校验设备与商户绑定关系是否一致 |
| `tbl_hardware_info` | N:1 | `device_id` | 设备硬件维度回溯 |
| `tbl_fiserv_batch` | 业务对应 | 时间窗 + `device_id` | 一次结算应覆盖该设备同期的批次记录 |
| `tbl_fiserv_sale_order` 等订单表 | 业务对应 | 时间窗 + `device_id` | 结算时段内的交易订单是结算金额的明细来源 |

## 校验点（QA 关注）

1. **追加表，不更新**：每条记录只读，每次结算完成后追加一条，**禁止 UPDATE** 历史记录；任何更新行为均视为异常。
2. **数据量持续增长**：建议按 `created_time` 或 `start_time` 做时间分区，避免历史表膨胀拖慢查询。
3. **`operator_id` 是审计字段**：必填，需校验来源的真实操作员（系统结算 vs 人工触发），不能为空或伪造。
4. **常用查询场景**：
   - 设备结算历史：按 `device_id` 过滤 + `start_time DESC` 排序 + `LIMIT 30`，关注无 `device_id` 索引时的性能；
   - 商户设备结算频率统计：按 `partner_id` 过滤 + `device_id` 分组，统计 `COUNT(*)`、`MIN(start_time)`、`MAX(end_time)`。
5. **时间字段一致性**：
   - `end_time` ≥ `start_time`；
   - `created_time` ≥ `end_time`（结算完成后才入库）；
   - 三者均使用毫秒精度 timestamp(3)，注意时区一致性。
6. **与 `t_pos_settlement` 的对应关系**：归档来源关系需保证 `device_id` 在主表中存在或曾经存在；同一 `device_id` + `start_time` 不应在主表与历史表同时存在（避免双写）。
7. **与商户/设备关系一致性**：`partner_id` 与 `device_id` 的对应关系应与 `tbl_merchant_device` 在结算时点的快照一致。
8. **与交易订单的金额对账**：在 POS 落库检查场景中，结算时段内 `tbl_fiserv_sale_order` 等订单表的合计应能与该次结算覆盖的批次（`tbl_fiserv_batch`）金额对齐。

## QA 落库检查要点

- **存在性**：每完成一次结算操作，应能在本表查到对应 `device_id` + `start_time` 的记录；
- **唯一性**：同一 `device_id` 不应出现 `start_time`/`end_time` 完全重复的多条记录；
- **审计完整性**：`operator_id`、`created_time` 非空，且 `created_time` 落在用例执行时间窗内；
- **跨表一致性**：与 `tbl_pos_settlement`、`tbl_fiserv_batch`、`tbl_fiserv_sale_order` 在 `device_id` 与时间窗维度对账无差异；
- **不可变性回归**：在用例后段尝试 UPDATE/DELETE 应被业务层禁止或不发生（视权限策略）。

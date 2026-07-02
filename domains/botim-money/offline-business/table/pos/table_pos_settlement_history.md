---
id: tbl_pos_settlement_history
object_type: Table
name: POS结算历史表(acquireii.t_pos_settlement_history)
aliases:
- t_pos_settlement_history
- acquireii.t_pos_settlement_history
domain: offline-business
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-06-25'
source_type: upload
source_ref: tables/t_pos_settlement_history.md
tags:
- pos
- settlement
- history
- archive
related_services: [svc_acquireii]
related_scenarios: []
---

# POS结算历史表(acquireii.t_pos_settlement_history)

## 用途
`acquireii.t_pos_settlement_history` 存储 POS 设备**已完成的结算记录**，是 POS 结算流水的归档表。每当一次设备结算(批结/对账)完成，即向本表追加一条只读记录，用于:按设备查询结算历史(设备维度审计)、按商户统计设备结算频率(商户维度运营分析)，与 [[tbl_pos_settlement]](活跃结算主表)配合承担长期归档职责。重要程度 ⭐⭐⭐。本表处于链路末端，是结算闭环的最终落点。

库表:`acquireii.t_pos_settlement_history`。

## 关联关系
- **所属服务**:[[svc_acquireii]](= frontmatter `related_services`)。
- **关键表**:[[tbl_pos_settlement]](`device_id` 归档来源主表)、[[tbl_merchant_device]](`device_id + partner_id` 校验设备-商户绑定)、[[tbl_hardware_info]](`device_id` 硬件维度回溯)、[[tbl_fiserv_batch]] / [[tbl_fiserv_sale_order]] 等(时间窗 + `device_id` 金额明细对账)。
- **哪些场景校验它**:POS 刷卡交易落库检查([[scn_pos_transaction_db_check]])。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint ✅ | 主键 |
| `device_id` | varchar(32) ✅ | 设备 ID，关联 [[tbl_hardware_info]] / [[tbl_merchant_device]] |
| `partner_id` | varchar(32) ✅ | 商户 ID |
| `start_time` | timestamp(3) ✅ | 结算开始时间 |
| `end_time` | timestamp(3) ✅ | 结算结束时间 |
| `operator_id` | varchar(50) ✅ | 操作员 ID(审计字段) |
| `created_time` | timestamp(3) ✅ | 创建时间(追加入库时刻) |

## 主键 / 索引
- 主键:`id`。
- 索引:当前仅主键索引;按 `device_id` / `partner_id` / `start_time` 查询场景下扫描成本较高，建议补建二级索引或时间分区(待补)。

## 校验点(QA 关注)
- **追加表，不更新**:每条记录只读，结算完成后追加一条，**禁止 UPDATE** 历史记录;任何更新行为均视为异常。
- **数据量增长**:建议按 `created_time` 或 `start_time` 做时间分区，避免历史表膨胀。
- **operator_id 审计**:必填，需校验真实操作员(系统结算 vs 人工触发)，不能为空或伪造。
- **时间字段一致性**:`end_time >= start_time`;`created_time >= end_time`(结算完成后才入库);均为毫秒精度 timestamp(3)，注意时区。
- **与主表对应关系**:`device_id` 在 [[tbl_pos_settlement]] 中应存在或曾经存在;同一 `device_id` + `start_time` 不应在主表与历史表同时存在(避免双写)。
- **金额对账**:结算时段内 [[tbl_fiserv_sale_order]] 等订单表合计应能与该次结算覆盖的批次([[tbl_fiserv_batch]])金额对齐。
- **存在性/唯一性**:每完成一次结算应能查到对应 `device_id` + `start_time` 记录;同一 `device_id` 不应出现 `start_time`/`end_time` 完全重复的多条记录。

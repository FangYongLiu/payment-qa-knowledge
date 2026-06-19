---
id: tbl_pos_settlement
object_type: Table
domain: device-pos
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_pos_settlement.md
tags:
- pos
- settlement
- 结算
subdomain: settlement
module: null
sensitivity: normal
name: POS结算表
aliases:
- t_pos_settlement
- acquireii.t_pos_settlement
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
记录 POS 设备的**结算操作**（日终结算 / 批结算）。POS 每天打烊时执行结算，系统统计当天交易、与 Fiserv / 卡组织对账，结算完成后才能产生最终的 Settlement Report。本表只存**活跃结算**，结算完成后会移至 `t_pos_settlement_history`。

典型场景：
- 收银员每天打烊前在 POS 上点"结算"
- 系统统计当天交易并对账
- 结算完成 → 生成 Settlement Report

## 关键列
| 字段 | 类型 | 说明 |
|------|------|------|
| `settlement_id` | bigint | 主键，结算 ID |
| `device_id` | varchar(32) | 设备 ID（唯一约束） |
| `partner_id` | varchar(32) | 商户 ID |
| `start_time` | timestamp(3) | 结算开始时间 |
| `end_time` | timestamp(3) | 结算结束时间 |
| `operator_id` | varchar(50) | 操作员 ID（谁执行的结算，用于审计） |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

所有字段均必填。

## 主键/索引
- PRIMARY：`settlement_id`
- `uk_ps_device`：`device_id` —— **唯一约束**，设备同时只能有一个活跃结算
- `i_ps_lut`：`last_updated_time` —— 按更新时间查询

## 校验点(QA 关注)
1. **device_id 唯一约束**：同一设备同一时刻只能存在一条活跃结算记录，重复插入应被拒绝。
2. **活跃结算 vs 历史**：结算完成后记录应从 `t_pos_settlement` 移至 `t_pos_settlement_history`，本表不应残留已完成结算。
3. **结算时间窗 [start_time, end_time]**：用于关联 `t_acquire_order`（device_id + created_time BETWEEN start_time AND end_time），需校验时间窗连续、不重叠。
4. **结算维度**：必须按设备维度执行，跨设备需分别结算。
5. **operator_id 审计**：必须记录执行结算的收银员，不可为空。
6. **partner_id 一致性**：与 device_id 所属商户应一致。
7. **data_version**：并发更新时应基于版本号控制。

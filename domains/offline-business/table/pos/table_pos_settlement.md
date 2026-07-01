---
id: tbl_pos_settlement
object_type: Table
name: POS结算表(acquireii.t_pos_settlement)
aliases:
- t_pos_settlement
- acquireii.t_pos_settlement
domain: offline-business
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-06-25'
source_type: upload
source_ref: tables/t_pos_settlement.md
tags:
- pos
- settlement
- 结算
related_services: [svc_acquireii]
related_scenarios: []
---

# POS结算表(acquireii.t_pos_settlement)

## 用途
`acquireii.t_pos_settlement` 记录 POS 设备的**活跃结算操作**(日终结算 / 批结算)。POS 每天打烊时由收银员发起结算，系统统计当天交易、与 Fiserv / 卡组织对账，结算完成后产生最终的 Settlement Report。本表只保存**进行中/活跃**的结算记录;结算完成后记录会被移至 [[tbl_pos_settlement_history]]，因此本表不应残留已完成结算。

库表:`acquireii.t_pos_settlement`。链路:刷卡交易(Fiserv 各订单表) → 按 `device_id` + `created_time` 归集 → 本表(收银员触发日终结算) → 对账成功 → [[tbl_pos_settlement_history]] → Settlement Report / Fiserv 批次([[tbl_fiserv_batch]])落地。

## 关联关系
- **所属服务**:[[svc_acquireii]](= frontmatter `related_services`)。
- **关键表**:[[tbl_pos_settlement_history]](结算完成后迁移)、[[tbl_merchant_device]](`device_id + partner_id` 校验设备-商户归属)、[[tbl_hardware_info]](`device_id` 设备基础信息)、[[tbl_fiserv_sale_order]] / [[tbl_fiserv_sale_void_ops_order]] / [[tbl_fiserv_refund_order]] / [[tbl_fiserv_reversal_order]](结算窗内交易)、[[tbl_fiserv_batch]](结算触发批次)、[[tbl_acquireii_t_acquire_order]](收单订单按结算窗归集)。
- **哪些场景校验它**:POS 刷卡交易落库检查([[scn_pos_transaction_db_check]])。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `settlement_id` | bigint | 主键，结算 ID |
| `device_id` | varchar(32) | 设备 ID(唯一约束，活跃期间唯一) |
| `partner_id` | varchar(32) | 商户 ID |
| `start_time` | timestamp(3) | 结算开始时间(结算窗左边界) |
| `end_time` | timestamp(3) | 结算结束时间(结算窗右边界) |
| `operator_id` | varchar(50) | 操作员 ID(执行结算的收银员，审计用) |
| `created_time` / `last_updated_time` | timestamp(3) | 创建/更新时间 |
| `data_version` | bigint | 数据版本(乐观锁) |

> 所有字段均必填。

## 主键 / 索引
- 主键:`settlement_id`。
- 索引:`uk_ps_device`(device_id，唯一约束——同一设备同时只能有一条活跃结算)、`i_ps_lut`(last_updated_time)。

## 校验点(QA 关注)
- **device_id 唯一约束**:同一设备同一时刻只能存在一条活跃结算记录，重复插入必须被 `uk_ps_device` 拒绝。
- **活跃 vs 历史分离**:结算完成后记录应从本表移至 [[tbl_pos_settlement_history]]，本表不应残留;QA 校验时需联查两表。
- **结算时间窗**:`[start_time, end_time]` 用于关联交易明细;需校验 `end_time >= start_time`、同一设备相邻结算窗连续不重叠不留空隙。
- **结算维度**:必须按设备(`device_id`)维度执行，不允许一条记录覆盖多设备。
- **operator_id 审计**:必须记录执行结算的收银员，不可为空。
- **partner_id 一致性**:必须与 [[tbl_merchant_device]] 中 `device_id` 所属商户一致。
- **data_version 并发控制**:更新基于乐观锁，避免并发结算覆盖。

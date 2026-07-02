---
id: tbl_reconciliation_t_transit_funds_flow
object_type: Table
name: 在途资金记录表 (t_transit_funds_flow)
aliases: [t_transit_funds_flow, reconciliation.t_transit_funds_flow]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: reconciliation schema DDL
tags: [settlement, reconciliation]
sensitivity: normal
related_services: []
---

# 在途资金记录表 (t_transit_funds_flow)

## 用途
物理表 `reconciliation.t_transit_funds_flow`,主键 `flow_id`。在途资金记录表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `flow_id` | bigint(17) | 主键 |
| `fund_channel_code` | varchar(16) | 渠道编号 |
| `biz_type` | varchar(4) | 业务类型 |
| `transit_date` | date | 在途日期 |
| `fund_in_amount` | decimal(15, 4) | 入款金额 · 可空 |
| `refund_amount` | decimal(15, 4) | 退款金额 · 可空 |
| `full_amount` | decimal(15, 4) | 渠道全额 · 可空 |
| `fee_amount` | decimal(15, 4) | 手续费金额 · 可空 |
| `vat_amount` | decimal(15, 4) | 增值税金额 · 可空 |
| `fundin_net_amount` | decimal(15, 4) | 入款净额 · 可空 |
| `estimated_arrival_date` | date | 预计到账日期 · 可空 |
| `actual_settelement_date` | date | Actual Settelement Date · 可空 |
| `settlement_delay_days` | int | Settlement Delay Days · 可空 |
| `bank_settle_amount` | decimal(15, 4) | 银行结算金额 · 可空 |
| `settle_diff_amount` | decimal(15, 4) | 结算差额 · 可空 |
| `adjust_amount` | decimal(15, 4) | 调账金额 · 可空 |
| `tobe_settle_amount` | decimal(15, 4) | 累计待结算金额 · 可空 |
| `currency` | varchar(3) | 币种 · 可空 |
| `operator` | varchar(32) | 操作人 · 可空 |
| `memo` | varchar(256) | 备注 · 可空 |
| `message` | varchar(128) | 操作信息 · 可空 |
| `transit_status` | varchar(4) | 报表状态 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |
| `outer_full_amount` | decimal(19, 4) | 外部全额 · 可空 |
| `outer_fee` | decimal(19, 4) | 外部手续费 · 可空 |
| `outer_fixed_fee` | decimal(19, 4) | 外部固定费 · 可空 |
| `outer_vat` | decimal(19, 4) | 外部VAT · 可空 |
| `outer_net_amount` | decimal(19, 4) | 外部净额 · 可空 |
| `day_cut_difference` | decimal(19, 4) | 日切差异 · 可空 |
| `day_cut_accumulation` | decimal(19, 4) | 累积日切 · 可空 |

## 主键 / 索引
- 主键:`flow_id`
- `uk_channel_transit_date`:fund_channel_code, transit_date (UNIQUE)
- `idx_estimated_arrival_date`:estimated_arrival_date

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

---
id: tbl_reconciliation_t_report_flow
object_type: Table
name: 报备交易列表 (t_report_flow)
aliases: [t_report_flow, reconciliation.t_report_flow]
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

# 报备交易列表 (t_report_flow)

## 用途
物理表 `reconciliation.t_report_flow`,主键 `flow_id`。报备交易列表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `flow_id` | bigint(17) | 主键 流水ID |
| `fund_channel_code` | varchar(32) | 渠道编号 |
| `biz_type` | varchar(4) | 业务类型 |
| `inst_order_no` | varchar(64) | 机构订单号 |
| `file_seq_no` | bigint(32) | 文件编号 · 可空 |
| `bill_date` | date | 对账日期 · 可空 |
| `trade_time` | timestamp | 交易日期 · 可空 |
| `amount` | decimal(15, 2) | 交易金额 · 可空 |
| `fee_amount` | decimal(15, 4) | 手续费 · 可空 |
| `vat_amount` | decimal(15, 4) | 增值税 · 可空 |
| `currency` | varchar(3) | 币种 · 可空 |
| `status` | varchar(8) | 状态 · 可空 |
| `bill_status` | varchar(8) | 对账状态 · 可空 |
| `message` | varchar(255) | 对账结果信息 · 可空 |
| `report_name` | varchar(64) | 交易报备人员 · 可空 |
| `operator` | varchar(64) | 操作者 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `accounting_flow_no` | varchar(32) | 登账关联单号 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |
| `settle_amount` | decimal(15, 4) | 结算金额 · 可空 |
| `settle_currency` | char(3) | 结算币种 · 可空 |
| `recon_extension` | varchar(512) | 对账扩展字段 · 可空 |
| `extension` | varchar(255) | 扩展信息 · 可空 |

## 主键 / 索引
- 主键:`flow_id`
- `uk_channel_inst_biz`:fund_channel_code, inst_order_no, biz_type (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

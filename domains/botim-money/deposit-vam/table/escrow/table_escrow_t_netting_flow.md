---
id: tbl_escrow_t_netting_flow
object_type: Table
name: 轧差后的用户明细表 (t_netting_flow)
aliases: [t_netting_flow, escrow.t_netting_flow]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: escrow schema DDL
tags: [deposit-vam, escrow]
sensitivity: normal
related_services: []
---

# 轧差后的用户明细表 (t_netting_flow)

## 用途
物理表 `escrow.t_netting_flow`,主键 `netting_flow_id`。轧差后的用户明细表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `netting_flow_id` | bigint(19) | id |
| `netting_batch_id` | bigint(19) | 批次号 · 可空 |
| `amount` | decimal(19, 4) | 金额 · 可空 |
| `direction` | varchar(4) | 金额方向 · 可空 |
| `card_no` | varchar(64) | 卡号 · 可空 |
| `flow_type` | varchar(4) | 流水类型 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |
| `currency` | varchar(8) | 币种 |
| `report_type` | varchar(8) | 上报类型,C-Credit,D-Debit |
| `embossed_english` | varchar(256) | 持卡人姓名 |
| `report_batch_id` | bigint(19) | 报送文件批次号 · 可空 |
| `report_date` | date | 报送的时间 · 可空 |

## 主键 / 索引
- 主键:`netting_flow_id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。

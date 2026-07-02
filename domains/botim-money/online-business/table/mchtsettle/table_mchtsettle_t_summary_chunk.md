---
id: tbl_mchtsettle_t_summary_chunk
object_type: Table
name: 汇总分片表 (t_summary_chunk)
aliases: [t_summary_chunk, mchtsettle.t_summary_chunk]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mchtsettle schema DDL
tags: [online-business, 商户结算, mchtsettle]
sensitivity: normal
related_services: [svc_merchant_settlement]
---

# 汇总分片表 (t_summary_chunk)

## 用途
物理表 `mchtsettle.t_summary_chunk`,主键 `id`。(DDL 未提供表注释)。属商户结算服务 [[svc_merchant_settlement]]。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:[[svc_merchant_settlement]](= `related_services`)。
- **谁读写它**:结算链路的服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `count` | bigint | count |
| `clearing_amount` | decimal(19,4) | clearing amount |
| `clearing_currency` | char(3) | clearing currency |
| `fee_amount` | decimal(19,4) | fee amount |
| `fee_currency` | char(3) | fee currency |
| `net_amount` | decimal(19,4) | net amount |
| `net_currency` | char(3) | net currency |
| `vat_amount` | decimal(19,4) | vat amount |
| `vat_currency` | char(3) | vat currency |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 金额比较用容差(< 0.01);amount 与对应 currency 成对、需一致。
- 更细的状态枚举、跨表关联与业务规则**待补**(需结合代码或业务文档)。
